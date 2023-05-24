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
        stage ("upload artefacts to nexus repository") {
            steps {
                script {

                    def readPomVersion = readMavenPom file: 'pom.xml'

                    def nexusRepo = readPomVersion.version.endsWith("SNAPSHOT") ? "counter-app-snap" : "counter-app"

                    nexusArtifactUploader artifacts: 
                    [
                        [
                            artifactId: 'springboot',
                            classifier: '',
                            file: 'target/Uber.jar',
                            type: 'jar'
                            ]
                    ], 
                    credentialsId: 'nexus-auth', 
                    groupId: 'com.example', 
                    nexusUrl: '3.111.38.239:8081/', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: nexusRepo, 
                    version: "${readPomVersion.version}"
                }
            }
        }
        stage ("Build docker image") {
            steps {
                script {
                    sh 'docker image build -t $JOB_NAME:v1.$BUILD_ID .'
                    sh 'docker image tag $JOB_NAME:v1.$BUILD_ID buban/$JOB_NAME:v1.$BUILD_ID'
                    sh 'docker image tag $JOB_NAME:v1.$BUILD_ID buban/$JOB_NAME:latest'
                }
            }
        }
    }
}
        













