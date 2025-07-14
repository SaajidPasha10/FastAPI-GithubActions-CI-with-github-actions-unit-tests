[![🔁 FastAPI CI](https://github.com/SaajidPasha10/FastAPI-GithubActions-CI-with-github-actions-unit-tests/actions/workflows/fastapi-ci.yml/badge.svg)](https://github.com/SaajidPasha10/FastAPI-GithubActions-CI-with-github-actions-unit-tests/actions/workflows/fastapi-ci.yml)

## 🚀 FastAPI CI/CD with GitHub Actions

This project demonstrates a complete CI pipeline for a FastAPI application using **GitHub Actions**. It includes:

- 📦 Dependency installation via `requirements.txt`
- ✅ Unit testing using **pytest**
- 📊 Code coverage reports via **pytest-cov**
- 🧪 HTML test report using **pytest-html**
- 🚀 Running the FastAPI server with **Uvicorn**
- 🌐 Endpoint health check via `curl`
- 📎 Uploading logs and test artifacts to GitHub

The pipeline ensures that your FastAPI app is tested, validated, and verifiable before deployment.

Github Actions explaination for this project can be found here [fastapi-ci.yml](.github/workflows/fastapi-ci.yml)

## 📂 Project Structure

```
├── main.py
├── requirements.txt
├── tests/
│ └── test_main.py
└── .github/
      └── workflows/
            └── fastapi-ci.yml
```

🔁 CI/CD Workflow Overview
The GitHub Actions workflow runs when you push or open a pull request on the main branch.

Steps:
✅ Checkout Code

🐍 Setup Python 3.11

📦 Install Dependencies

🧪 Run Tests + HTML Coverage Report

📎 Upload pytest Report Artifacts

🚀 Start FastAPI server in background

🌐 Test / endpoint using curl

📎 Upload server.log

Test Reports can be found here

Actions > Last Workflow Run > Artifacts
<img width="926" height="436" alt="image" src="https://github.com/user-attachments/assets/77a71130-e4ba-4581-8484-8905260e4a4f" />


📄 pytest-html-and-coverage

📄 server-log

You can download and open report.html and coverage results from there.
