pipeline {
    agent any 
    stages {
        stage ('Fetch Code') {
            steps {
                git branch: 'main', url: 'https://github.com/rigveda007/demo-counter-app.git'
            }
        }
    }
}