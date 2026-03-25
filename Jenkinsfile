pipeline {
    agent any 

    environment {
        // 1. CHANGE 'your-dockerhub-username' to your actual Docker Hub ID
        DOCKERHUB_CREDENTIALS = 'docker-hub-credentials'
        // 2. This MUST match the ID you created in Jenkins Credentials "Safe"
       IMAGE_NAME = 'pavani2405/new_docker_image'
    }


    stages {

        stage('Build Java Application') {
            steps {
                bat 'javac HelloWorld.java'
            }
        }

        stage('Run Java Program') {
            steps {
                bat 'java HelloWorld'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME%:latest .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(
                credentialsId: 'Docker-credentials',
                usernameVariable: 'USER',
                passwordVariable: 'PASS')]) {

                    bat 'echo %PASS% | docker login -u %USER% --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker push %IMAGE_NAME%:latest'
            }
        }
    }
}
