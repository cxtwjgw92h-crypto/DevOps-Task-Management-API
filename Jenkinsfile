
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building Task Management API'
                bat 'mvn clean package'
            }
        }

        stage('Version Artifact') {
            steps {
                bat "copy /Y target\\task-management-api-0.0.1-SNAPSHOT.jar target\\task-management-api-${env.BUILD_NUMBER}.jar"
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/task-management-api-*.jar',
                                 fingerprint: true
            }
        }
    }
}
