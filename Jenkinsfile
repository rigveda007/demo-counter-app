pipeline {
    agent any 
    stages {
        stage ('Fetch Code') {
            steps {
                git branch: 'main', url: 'https://github.com/rigveda007/demo-counter-app.git'
            }
        }
        stage ('Unit Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage ('Integration Testing') {
            steps {
                sh 'mvn verify -DskipUnitTests'
            }
        }
        stage ('Code Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage ('Sonarqube Analysis') {
            steps {
                script {
                      withSonarQubeEnv(credentialsId: 'sonar-api') {
                        sh 'mvn clean package sonar:sonar'
                   }
                }
              
          }
        }
        stage ('Quality Gate Test') {
            steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api'
                }
            }
        }
    }
}















