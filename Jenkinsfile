pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "tanvirmulla11/gradle-java-app"
    }

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/tanvirmulla11/Java-Application-Using-Gradle.git'
            }
        }

        stage('Build with Gradle') {
            steps {
                sh './gradlew clean build'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker run -d -p 8080:8080 $DOCKER_IMAGE'
            }
        }
    }
}
