pipeline {
    agent any 
    stages {
        stage ('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/rigveda007/demo-counter-app.git'
            }
        }
        stage ('Unit Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage ('Integration Test') {
            steps {
                sh 'mvn verify -DskipUnitTests'
            }
        }
        stage ('Code Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage ('Static Code Analysis') {
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'sonar-api') {
                      sh 'mvn clean package sonar:sonar'
                  }
                }
            }
        }
        stage ('Upload to Nexus') {
            steps {
                script {
                    nexusArtifactUploader artifacts: 
                    [
                       [
                         artifactId: 'springboot',
                         classifier: '', file: 'target/Uber.jar',
                         type: 'jar'
                         ]
                    ], 
                    credentialsId: 'nexus-auth', 
                    groupId: 'com.example', 
                    nexusUrl: '13.234.75.44:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'demoapp-release', 
                    version: '1.0.0'
                }
            }
        }

    }   
}















