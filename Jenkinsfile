pipeline {
    agent any 
    stages {
        stage ("Git Checkout") {
            steps {
                git branch: 'main', url: 'https://github.com/rigveda007/demo-counter-app.git'
            }
        }
        stage ("Unit Test") {
            steps {
                sh 'mvn test'
            }
        }
        stage ("Integration Test") {
            steps {
                sh 'mvn verify -DskipUnitTests'
            }
        }
        stage ("Code Build") {
            steps {
                sh 'mvn clean install'
            }
        }
        stage ("Static Code Analysis") {
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'sonar-api') {
                        sh 'mvn clean package sonar:sonar'
                  }
                }
            }
        }
        
    }
}














