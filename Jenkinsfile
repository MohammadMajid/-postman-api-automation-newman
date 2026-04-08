pipeline {
  agent any

  options {
    timestamps()
    buildDiscarder(logRotator(numToKeepStr: '20'))
  }

  environment {
    COLLECTION_FILE = 'bookstore.postman_collection.json'
    ENV_FILE = 'qa.postman_environment.json'
    REPORTS_DIR = 'reports'
    ALLURE_RESULTS_DIR = 'allure-results'
    ALLURE_REPORT_DIR = 'public'
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Prepare Tooling') {
      steps {
        sh '''
          set -eu
          node --version
          npm --version
          java -version
          npm install -g newman newman-reporter-htmlextra newman-reporter-allure allure-commandline
        '''
      }
    }

    stage('Run API Tests') {
      steps {
        sh '''
          set +e
          mkdir -p "$REPORTS_DIR" "$ALLURE_RESULTS_DIR" "$ALLURE_REPORT_DIR"

          newman run "$COLLECTION_FILE" \
            -e "$ENV_FILE" \
            --reporters cli,htmlextra,junit,allure \
            --reporter-htmlextra-export "$REPORTS_DIR/newman-report.html" \
            --reporter-junit-export "$REPORTS_DIR/junit-report.xml" \
            --reporter-allure-export "$ALLURE_RESULTS_DIR"

          NEWMAN_EXIT_CODE=$?
          printf '%s' "$NEWMAN_EXIT_CODE" > .newman-exit-code
          exit 0
        '''
      }
    }

    stage('Generate Allure Report') {
      steps {
        sh '''
          set +e
          allure generate "$ALLURE_RESULTS_DIR" --clean -o "$ALLURE_REPORT_DIR"
          exit 0
        '''
      }
    }

    stage('Evaluate Test Result') {
      steps {
        script {
          def newmanExitCode = readFile('.newman-exit-code').trim()
          if (newmanExitCode != '0') {
            error("Newman execution failed with exit code ${newmanExitCode}")
          }
        }
      }
    }
  }

  post {
    always {
      junit allowEmptyResults: true, testResults: 'reports/junit-report.xml'
      archiveArtifacts allowEmptyArchive: true, artifacts: 'reports/**, allure-results/**, public/**'
    }
  }
}
