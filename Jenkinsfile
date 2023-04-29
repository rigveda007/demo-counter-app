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
                sh "mvn test"
            }
        }
        stage ('Integretion Testing') {
            steps {
                sh 'mvn verify -DskipUnitTests'
            }
        }
    }
}
