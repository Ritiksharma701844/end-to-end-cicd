pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/Ritiksharma701844/end-to-end-cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t simpleweb .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 8082:80 simpleweb || true'
            }
        }

    }
}
