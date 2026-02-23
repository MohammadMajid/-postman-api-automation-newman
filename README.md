# Postman API Automation - GitLab CI/CD

This project runs Postman collections automatically using GitLab pipelines.

## Features

- Newman CLI Execution
- Environment Support
- HTML Reporting
- CI/CD Integration

## Run Locally

Install newman:

npm install -g newman

Run:

newman run tests/bookstore.postman_collection.json -e tests/qa.postman_environment.json

## Pipeline

Automatically runs on push.