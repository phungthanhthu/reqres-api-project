pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/phungthanhthu/reqres-api-project.git'
            }
        }

        stage('Install Newman') {
            steps {
                bat 'npm install -g newman'
            }
        }

        stage('Run Positive Tests') {
            steps {
                bat 'newman run reqres-positive-collection.json -r cli,html --reporter-html-export positive-report.html'
            }
        }

        stage('Run Negative Tests') {
            steps {
                bat 'newman run reqres-negative-collection.json -r cli,html --reporter-html-export negative-report.html --suppress-exit-code'
            }
        }

        stage('Archive Reports') {
            steps {
                archiveArtifacts artifacts: '*.html', fingerprint: true
                publishHTML([target: [
                    reportDir: '.', 
                    reportFiles: 'positive-report.html,negative-report.html',
                    reportName: 'Newman Test Reports'
                ]])
            }
        }
    }
}
