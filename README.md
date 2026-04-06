# 🚀 Enterprise API Automation Framework

⭐ Designed to demonstrate enterprise API automation and DevOps CI/CD practices.

Enterprise-grade API automation framework demonstrating Senior QA Automation and DevOps CI/CD practices using Postman Collections executed via Newman CLI inside GitHub Actions and GitLab CI/CD.
This project showcases secure automation workflows, dynamic token handling, and advanced enterprise reporting dashboards.

## ⭐ Key Features

- ✅ Automated API Validation using Postman Collections
- ✅ GitHub Actions CI/CD Pipeline Execution
- ✅ GitLab CI/CD Pipeline Execution
- ✅ Dynamic Token Management
- ✅ Secure Secrets Handling
- ✅ HTML Evidence Reporting
- ✅ GitHub Native Test Analytics (JUnit)
- ✅ JSON Metrics Output for Monitoring Tools
- ✅ Allure Dashboard Visualization (Graphs + Trends)

## 🧰 Technology Stack

- Postman
- Newman CLI
- GitHub Actions
- GitLab CI/CD
- NodeJS
- JavaScript
- Allure Reporting
- JUnit Analytics

## 🏗️ Architecture Overview

```
Developer Push / Merge Request
      ↓
GitHub Actions or GitLab Pipeline Triggered
      ↓
CI Runner (Node Docker Image)
      ↓
Newman API Execution
      ↓
Assertions + Validation
      ↓
Reports Generated
   ├── HTML Evidence Report
   ├── GitHub Test Analytics (JUnit)
   ├── JSON Metrics Output
   └── Allure Dashboard
```

## 📂 Repository Structure

```
postman-api-automation/
├── .github/workflows/ci.yml
├── .gitlab-ci.yml
├── .gitignore
├── README.md
├── bookstore.postman_collection.json
└── qa.postman_environment.json
```

## ▶️ Local Execution

Install Newman:

```sh
npm install -g newman
npm install -g newman-reporter-htmlextra
npm install -g newman-reporter-allure
npm install -g allure-commandline
```

`junit` is a built-in Newman reporter, so there is no `newman-reporter-junit` package to install.

Run collection locally:

```sh
newman run bookstore.postman_collection.json \
      -e qa.postman_environment.json
```

## ⚙️ GitHub Actions CI/CD Pipeline

Pipeline automatically executes when:
- Code is pushed
- Pull Requests are created

Pipeline performs:
- Newman installation
- API execution
- Assertion validation
- Multi-format report generation

GitHub Pages deployment is opt-in. Set the repository variable `ENABLE_GITHUB_PAGES=true` only after Pages has been enabled in the repository settings and configured for GitHub Actions.

Automated report email is also opt-in. Configure these repository variables and secrets before enabling it:

- Variables:
      - `ENABLE_REPORT_EMAIL=true`
      - `REPORT_EMAIL_TO=<recipient@example.com>` (optional, defaults to `mohammadnafiulmajid@gmail.com`)
      - `REPORT_EMAIL_FROM=<sender@example.com>` (optional, defaults to `SMTP_USERNAME`)
- Secrets:
      - `SMTP_SERVER`
      - `SMTP_PORT`
      - `SMTP_USERNAME`
      - `SMTP_PASSWORD`

## ⚙️ GitLab CI/CD Pipeline

The GitLab pipeline is defined in `.gitlab-ci.yml` and runs when:
- Code is pushed
- Merge Requests are created or updated

Pipeline performs:
- Newman installation
- Java 17 runtime setup for Allure generation
- API execution
- Assertion validation
- JUnit, HTML Extra, and Allure report generation
- Artifact publishing for reports and Allure output

GitLab test results are published from `reports/junit-report.xml` and can be viewed in the pipeline test report UI.

GitLab Pages deployment is opt-in. Enable GitLab Pages for the project, then set this CI/CD variable before expecting the `pages` job to run:

- `ENABLE_GITLAB_PAGES=true`

Automated report email is also opt-in for GitLab. Configure these CI/CD variables before enabling it:

- Required variables:
      - `ENABLE_REPORT_EMAIL=true`
      - `SMTP_SERVER`
      - `SMTP_PORT`
      - `SMTP_USERNAME`
      - `SMTP_PASSWORD`
- Optional variables:
      - `REPORT_EMAIL_TO=<recipient@example.com>` (defaults to `mohammadnafiulmajid@gmail.com`)
      - `REPORT_EMAIL_FROM=<sender@example.com>` (defaults to `SMTP_USERNAME`)

When enabled on the `main` branch:
- `api_tests` always runs for push and merge request pipelines
- `pages` publishes the generated Allure site from `public/`
- `email_report` sends a zipped copy of the Allure report as an attachment

## 📊 Advanced Reporting (Enterprise Setup)

The pipeline generates multiple reporting formats similar to large fintech and streaming platform QA workflows.

### ✅ HTML Evidence Report
- **Location:** `reports/newman-report.html`
- **Includes:** Request details, Response payloads, Assertion results, Failure diagnostics
- **Download via:** Workflow run → Artifacts

### ✅ GitHub Test Analytics (JUnit)
- **JUnit reporting enables native GitHub visibility.**
- **Displays:** Passed Tests, Failed Tests, Execution Duration
- **Accessible inside:** Actions → Workflow run → Test Report

### ✅ GitLab Test Report (JUnit)
- **JUnit reporting enables native GitLab visibility.**
- **Displays:** Passed Tests, Failed Tests, Execution Duration
- **Accessible inside:** CI/CD → Pipelines → Tests

### ✅ JSON Metrics Output
- **Machine-readable reporting:** `reports/result.json`
- **Future integrations:** Datadog, Grafana, ELK Stack, Custom dashboards

### ✅ Allure Dashboard
- **Generated automatically during pipeline execution.**
- **Provides:** Visual test analytics, Trend analysis, Failure grouping, Historical debugging insights
- **Artifact:** `allure-report/`
- **Download from workflow artifacts.**

## 🔐 Dynamic Runtime Secrets

The framework automatically extracts runtime values from API responses:
- `authToken`
- `tokenExpiry`
- `userID`
- `username`

Example:
```js
pm.environment.set("authToken", body.token);
pm.environment.set("tokenExpiry", body.expires);
```

Secrets may rotate periodically without requiring repository changes.

**Security Practices:**
- Masked GitHub Secrets
- Masked GitLab CI/CD Variables
- No credentials stored in Git history
- Environment-driven execution

## 📈 Future Enhancements

- Playwright API Integration
- Slack Failure Notifications
- Datadog Metrics Publishing
- Dockerized Newman Runner
- Parallel Pipeline Execution

## 📄 License

MIT License

## 👨‍💻 Author

Mohammad Majid  
Senior QA Automation Engineer | Cloud CI/CD Automation

⭐ Designed to demonstrate enterprise API automation, secure pipelines, and advanced DevOps reporting workflows.
