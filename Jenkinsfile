pipeline {
    agent any

    environment {
        IMAGE_NAME = 'mahithareddy/myapp' 
    }

    stages {
        stage('Clone') {
            steps {
                url: 'https://github.com/Mahitha-Work/tomcat-maven-cicd.git', brnach: 'master'
            }
        }

        stage('Build WAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin'
                    sh 'docker push $IMAGE_NAME'
                }
            }
        }
    }
}
