pipeline {
    agent any

    /* If 'mvn' is already installed on your Jenkins server 
       globally, you can delete the 'tools' block entirely.
    */
    tools {
        maven 'maven' // Change 'maven' to your Jenkins Tool Name
        jdk 'jdk'     // Change 'jdk' to your Jenkins Tool Name
    }

    stages {
        stage('Checkout') {
            steps {
                // 'checkout scm' is the most reliable way to avoid branch errors
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
            // This captures your .jar file so you can see it in Jenkins
            archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: true
        }
        failure {
            echo 'Build Failed. Check the console output above.'
        }
    }
}
