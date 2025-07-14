# 📘 GitHub Actions Workflow – Explained [fastapi-ci.yml](.github/workflows/fastapi-ci.yml)

This document explains your GitHub CI pipeline for a FastAPI app. The workflow installs dependencies, runs tests with coverage and HTML report, launches the server, tests the `/` endpoint, and uploads logs and test reports.

---

## 🧪 Trigger Conditions

```yaml
on:
  push:
    branches: [ main ]
  pull_request:
```
Triggered when code is pushed to main

Also runs on pull requests to main

🔧 Job Configuration
```
jobs:
  build:
    runs-on: ubuntu-latest
```
Job is called build

Runs on GitHub-hosted Ubuntu machine

STEP 1 - Pulls your repo so the runner can access your files

📥 Checkout Code
```
- name: 📥 Checkout code
  uses: actions/checkout@v4
```

STEP 2 - 🐍 Set Up Python
Installs Python 3.11 on the runner

You can change this version if needed

```
- name: 🐍 Set up Python
  uses: actions/setup-python@v4
  with:
    python-version: '3.11'
```

STEP 3 - 📦 Install Dependencies

Upgrades pip

Installs everything from your requirements.txt

```
- name: 📦 Install dependencies
  run: |
    python -m pip install --upgrade pip
    pip install -r requirements.txt

```

STEP 4 - 🧪 Run Tests + Coverage + HTML Report

mkdir -p test-results: Create directory to store reports

--cov=main: Track code coverage for main.py

--cov-report=term: Shows summary in logs

--cov-report=html: Saves detailed coverage HTML inside htmlcov

--html: Saves a beautiful HTML summar

```
- name: 🧪 Run Unit Tests with Coverage and HTML Report
  run: |
    mkdir -p test-results
    pytest tests/ \
      --cov=main \
      --cov-report=term \
      --cov-report=html:test-results/htmlcov \
      --html=test-results/report.html
```

STEP 5 - 📎 Upload Test Artifacts

Saves the coverage + HTML report so you can download it from GitHub UI

```
- name: 📎 Upload Test Report Artifacts
  uses: actions/upload-artifact@v4
  with:
    name: pytest-html-and-coverage
    path: test-results/
```

STEP 6 - 🚀 Start FastAPI Server

nohup runs server in background

Logs go to server.log

sleep 10 waits 10 seconds for server to be ready

```
- name: 🚀 Start FastAPI server
  run: |
    nohup uvicorn main:app --host 0.0.0.0 --port 8000 > server.log 2>&1 &
    sleep 10
```

Finally ✅ Hit the / Endpoint

Sends HTTP request to http://localhost:8000

If status is not 2xx, fails with error message

```
- name: ✅ Test / endpoint with curl
  run: |
    curl --fail http://localhost:8000 || (echo "❌ Server did not respond!" && exit 1)
```

📎 Upload Server Log

```
- name: 📎 Upload server log
  uses: actions/upload-artifact@v4
  with:
    name: server-log
    path: server.log
```

Uploads server.log so you can review FastAPI output from GitHub UI

