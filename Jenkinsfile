pipeline {
    agent any
    tools{
        maven 'Maven'
    }
    stages {
        stage (SCM) {
            steps {
                git branch: 'main', url: 'https://github.com/aitharoshankumar/pet_shop.git'
            }
        }
        stage (build) {
            steps {
                sh 'mvn clean package'
            }
        }
        stage (deploy) {
            steps {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'deployer', path: '', url: 'http://13.60.94.47:8080/')], contextPath: null, war: 'target/petshop.war'
            }
        }
    }
}
