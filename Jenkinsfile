pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/Parasharam-DevOps/Test-CICD.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t cicd-docker-app .'
            }
        }

        stage('Tag Docker Image') {
            steps {
                sh 'docker tag cicd-docker-app parasharam0915/cicd-app:${BUILD_NUMBER}'
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push parasharam0915/cicd-app:${BUILD_NUMBER}'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker stop cicd-container || true'
                sh 'docker rm cicd-container || true'
                sh 'docker run -d -p 8000:80 --name cicd-container parasharam0915/cicd-app:${BUILD_NUMBER}'
            }
        }

    }
}
