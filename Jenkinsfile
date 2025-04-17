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
                bat 'newman run reqres-positive-collection.json'
            }
        }

        stage('Run Negative Tests') {
            steps {
                // Dùng --suppress-exit-code để không fail pipeline nếu test này fail (vì negative thường fail mà đúng)
                bat 'newman run reqres-negative-collection.json --suppress-exit-code'
            }
        }
    }
}
