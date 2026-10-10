pipeline {
    agent any

    environment {
        JAVA_HOME = 'C:\\Program Files\\Java\\jdk-21.0.12.1'
        PATH = "${JAVA_HOME}\\bin;${env.PATH}"
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
                echo 'GitHub source code checked out successfully'
            }
        }

        stage('Check Java and Docker') {
            steps {
                bat 'echo JAVA_HOME=%JAVA_HOME%'
                bat 'java -version'
                bat 'javac -version'
                bat 'docker --version'
            }
        }

        stage('Build Spring Boot Application') {
            steps {
                bat 'mvnw.cmd clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t springboot-k8s-demo:1.0 .'
            }
        }
    }

    post {
        success {
            echo 'SUCCESS: Spring Boot application and Docker image built!'
        }

        failure {
            echo 'BUILD FAILED: Check the Jenkins console output.'
        }
    }
}