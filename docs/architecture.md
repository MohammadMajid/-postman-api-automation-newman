# 🏗 API Automation Architecture

## Overview

This project implements enterprise-style API automation using Postman Collections executed through Newman CLI inside GitLab CI/CD pipelines.

The framework focuses on secure execution, dynamic authentication handling, and advanced reporting visibility.

---

# System Flow

```
Developer Push
      ↓
GitLab Pipeline Triggered
      ↓
CI Runner (Node Docker Image)
      ↓
Newman CLI Execution
      ↓
API Requests Executed
      ↓
Assertions + Validations
      ↓
Multi-Format Reports Generated
```

---

# Authentication Strategy

Authentication tokens are dynamically generated during pipeline execution.

Workflow:

1. Create User API executes.
2. Username and UserID stored as environment variables.
3. Token generated via authorization API.
4. Token reused across secured API requests.

Example:

```
pm.environment.set("authToken", body.token);
pm.environment.set("tokenExpiry", body.expires);
```

This prevents hardcoded credentials.

---

# Secrets Management

Sensitive values are managed using GitLab CI/CD Variables.

Location:

GitLab → Settings → CI/CD → Variables

Examples:

* API_TOKEN
* USERNAME
* PASSWORD

Secrets are masked and protected.

No credentials are committed to repository history.

---

# CI/CD Execution

Pipeline uses:

* Node Docker Image
* Newman CLI
* Multiple Reporters

Execution includes:

* Dependency installation
* Collection execution
* Validation checks
* Artifact generation

Pipeline fails automatically when assertions fail.

---

# Reporting Architecture

Multiple reporting formats provide visibility.

## HTML Report

Human-readable audit evidence.

Contains:

* Request payloads
* Response payloads
* Assertion failures

Location:

```
reports/newman-report.html
```

---

## GitLab Test Analytics (JUnit)

JUnit XML integrates directly into GitLab UI.

Displays:

* Pass/Fail count
* Duration
* Failure tracking.

---

## JSON Metrics

Machine-readable results for monitoring integrations.

Future integrations:

* Datadog
* Grafana
* ELK Stack.

---

## Allure Dashboard

Provides:

* Failure grouping
* Trend analysis
* Historical debugging.

Generated during pipeline execution.

---

# Environment Strategy

Environment variables allow execution across multiple environments.

Examples:

* QA
* Staging
* Production.

Postman environments enable configuration reuse without modifying collections.

---

# Future Architecture Enhancements

* Playwright API Integration
* Dockerized Execution
* Parallel Pipeline Execution
* Slack Notifications
* Observability Integration (Datadog)

---

⭐ Designed to demonstrate enterprise API automation and DevOps CI/CD practices.
