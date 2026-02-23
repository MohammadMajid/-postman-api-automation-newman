⭐ Designed to demonstrate enterprise API automation and DevOps CI/CD practices.


# 🚀 Enterprise API Automation Framework

### Postman + Newman + GitLab CI/CD | Advanced Reporting Enabled

Enterprise-grade API automation framework demonstrating **Senior QA Automation** and **DevOps CI/CD practices** using Postman Collections executed via **Newman CLI** inside **GitLab Pipelines**.

This project showcases secure automation workflows, dynamic token handling, and **advanced enterprise reporting dashboards**.

---

# ⭐ Key Features

✅ Automated API Validation using Postman Collections
✅ GitLab CI/CD Pipeline Execution
✅ Dynamic Token Management
✅ Secure Secrets Handling
✅ HTML Evidence Reporting
✅ GitLab Native Test Analytics (JUnit)
✅ JSON Metrics Output for Monitoring Tools
✅ Allure Dashboard Visualization (Graphs + Trends)

---

# 🧰 Technology Stack

* Postman
* Newman CLI
* GitLab CI/CD
* NodeJS
* JavaScript
* Allure Reporting
* JUnit Analytics

---

# 🏗 Architecture Overview

```
Developer Push
      ↓
GitLab Pipeline Triggered
      ↓
CI Runner (Node Docker Image)
      ↓
Newman API Execution
      ↓
Assertions + Validation
      ↓
Reports Generated
   ├── HTML Evidence Report
   ├── GitLab Test Analytics (JUnit)
   ├── JSON Metrics Output
   └── Allure Dashboard
```

---

# 📂 Repository Structure

```
postman-api-automation/

├── .gitlab-ci.yml
├── README.md
├── package.json
├── .gitignore
│
├── tests/
│   ├── collections/
│   │      └── bookstore.postman_collection.json
│   │
│   └── environments/
│          └── qa.postman_environment.json
│
├── reports/
│
└── docs/
      └── architecture.md
```

---

# ▶️ Local Execution

Install Newman:

```
npm install -g newman
```

Run collection locally:

```
newman run tests/bookstore.postman_collection.json \
-e tests/qa.postman_environment.json
```

---

# ⚙️ GitLab CI/CD Pipeline

Pipeline automatically executes when:

* Code is pushed
* Merge Requests are created

Pipeline performs:

* Newman installation
* API execution
* Assertion validation
* Multi-format report generation

---

# 📊 Advanced Reporting (Enterprise Setup)

The pipeline generates multiple reporting formats similar to large fintech and streaming platform QA workflows.

## Generated Reports

### ✅ HTML Evidence Report

Location:

```
reports/newman-report.html
```

Includes:

* Request details
* Response payloads
* Assertion results
* Failure diagnostics

Download via:

```
Pipeline → Job → Artifacts
```

---

## ✅ GitLab Test Analytics (JUnit)

JUnit reporting enables native GitLab visibility.

Displays:

* Passed Tests
* Failed Tests
* Execution Duration

Accessible inside:

```
CI/CD → Job → Tests Tab
```

---

## ✅ JSON Metrics Output

Machine-readable reporting:

```
reports/result.json
```

Future integrations:

* Datadog
* Grafana
* ELK Stack
* Custom dashboards

---

## ✅ Allure Dashboard

Generated automatically during pipeline execution.

Provides:

* Visual test analytics
* Trend analysis
* Failure grouping
* Historical debugging insights

Artifact:

```
allure-report/
```

Download from pipeline artifacts.

## Dynamic Runtime Secrets

The framework automatically extracts runtime values from API responses:

* authToken
* tokenExpiry
* userID
* username

Example:

```
pm.environment.set("authToken", body.token);
pm.environment.set("tokenExpiry", body.expires);
```

Secrets may rotate periodically without requiring repository changes.

Security Practices:

* Masked GitLab Variables
* No credentials stored in Git history
* Environment-driven execution

---

# 📈 Future Enhancements

* Playwright API Integration
* Slack Failure Notifications
* Datadog Metrics Publishing
* Dockerized Newman Runner
* Parallel Pipeline Execution

---

# 📄 License

MIT License

---

# 👨‍💻 Author

Mohammad Majid
Senior QA Automation Engineer | Cloud CI/CD Automation

---

⭐ Designed to demonstrate enterprise API automation, secure pipelines, and advanced DevOps reporting workflows.
