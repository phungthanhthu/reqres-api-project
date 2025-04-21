pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/phungthanhthu/reqres-api-project.git'
            }
        }

        stage('Install Newman + Reporter') {
            steps {
                bat 'npm install -g newman'
                bat 'npm install -g newman-reporter-htmlextra'
            }
        }

        stage('Run Positive Tests') {
            steps {
                bat 'newman run reqres-positive-collection.json -r htmlextra --reporter-htmlextra-export reports/positive-report.html'
            }
        }

        stage('Run Negative Tests') {
            steps {
                bat 'newman run reqres-negative-collection.json -r htmlextra --reporter-htmlextra-export reports/negative-report.html --suppress-exit-code'
            }
        }
    }

    post {
        always {
            publishHTML([
                reportDir: 'reports',
                reportFiles: 'positive-report.html,negative-report.html',
                reportName: 'Newman Test Reports',
                keepAll: true,
                alwaysLinkToLastBuild: true
            ])
        }
    }
}
