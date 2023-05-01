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
        stage ('Maven Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Static code analysis') {
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