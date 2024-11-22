pipeline {
    agent any
    environment {
        SEMGREP_APP_TOKEN = credentials('semgrep-token') // Ensure 'semgrep-token' matches the ID you used
    }
    tools {
        jdk 'Java11' // Ensure this matches the JDK installation name in Jenkins
        maven 'maven3' // Ensure this matches the Maven installation name in Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Padma-priya746/Railway-Reservation-Application.git'
            }
        }
        stage('Build') {
            steps {
                dir('path/to/your/project') { // Change this to the actual path where pom.xml is located
                    sh 'mvn clean compile' // Compile the project using Maven
                }
            }
        }
        stage('Install Semgrep') {
            steps {
                sh 'pip install semgrep' // Install Semgrep using pip
            }
        }
        stage('Run Semgrep') {
            steps {
                sh 'semgrep --config auto --auth-token $SEMGREP_APP_TOKEN > semgrep-output.txt' // Run Semgrep scan
            }
        }
        stage('Archive Results') {
            steps {
                archiveArtifacts artifacts: 'semgrep-output.txt', allowEmptyArchive: true // Archive the Semgrep results
            }
        }
    }
    post {
        always {
            script {
                if (fileExists('semgrep-output.txt')) {
                    echo 'Semgrep scan completed, displaying results:'
                    sh 'cat semgrep-output.txt'
                } else {
                    echo 'No Semgrep output found.'
                }
            }
        }
    }
}
