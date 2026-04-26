pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "srajju0723b/myapp"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/vvce23ise0246-star/dem.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:latest")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-creds') {
                        docker.image("${DOCKER_IMAGE}:latest").push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Image successfully built and pushed'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}
