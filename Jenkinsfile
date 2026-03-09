pipeline {
    agent any

    tools {
        sonarScanner 'sonar-scanner'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/Ritiksharma701844/end-to-end-cicd.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh '''
                    sonar-scanner \
                    -Dsonar.projectKey=end-to-end-cicd \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=http://13.201.167.133:9000 \
                    -Dsonar.login=$SONAR_AUTH_TOKEN
                    '''
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t simpleweb .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker rm -f simpleweb || true
                docker run -d --name simpleweb -p 8082:80 simpleweb
                '''
            }
        }
    }
}