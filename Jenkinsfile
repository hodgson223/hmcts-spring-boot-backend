pipeline {
    agent any

    stages {
        stage('Check Java') {
            steps {
                bat 'java -version'
            }
        }

        stage('Build Spring App') {
            steps {
                bat 'gradlew.bat build'
            }
        }
    }

    post {
        success {
            echo 'Spring Boot build successful.'
        }
        failure {
            echo 'Build failed.'
        }
    }
}