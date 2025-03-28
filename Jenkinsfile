pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "akshathaharish/helloworld-app"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/AkshathaMR/hello-world-war.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                withDockerRegistry([credentialsId: 'dockerhub-credentials', url: '']) {
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }

        stage('Deploy Application') {
            steps {
                sh 'docker run -d --name helloworld -p 8090:8080 $DOCKER_IMAGE'
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful!'
        }
        failure {
            echo 'Deployment Failed!'
        }
    }
}
