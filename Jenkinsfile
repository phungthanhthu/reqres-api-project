pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/phungthanhthu/reqres-api-project.git'
            }
        }

        stage('Install Newman') {
            steps {
                bat 'npm install -g newman'
            }
        }

        stage('Run API Tests') {
            steps {
                bat 'newman run reqres-collection.json'
            }
        }
    }
}
