pipeline {
    agent any
    environment {
        IMAGE_NAME = "petshop-tomcat"
        CONTAINER_NAME = "petshop"
        HOST_PORT = "7070"
        CONTAINER_PORT = "8080"
    }
    stages {
        stage (SCM) {
            steps {
                git branch: 'main', url: 'https://github.com/vamsibyramala/pet_shop.git'
            }
        }
        stage (build) {
            steps {
                sh 'mvn clean package'
            }
        }
        stage (deploy) {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://13.127.16.29:8081/')], contextPath: 'test', war: '**/*.war'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p $HOST_PORT:$CONTAINER_PORT --name $CONTAINER_NAME $IMAGE_NAME'
            }
        }
    }
}
