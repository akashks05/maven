pipeline {
    agent any

    tools {
        // Ensure these match your "Global Tool Configuration" names
        maven 'Maven3' 
        jdk   'JDK17'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Cleaning and Compiling...'
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                echo 'Running Unit Tests...'
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                echo 'Creating JAR file...'
                sh 'mvn package -DskipTests'
            }
        }
    }

    post {
        success {
            echo 'Build Successful!'
            archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: true
        }
        failure {
            echo 'Build Failed. Check the console output above.'
        }
    }
}
