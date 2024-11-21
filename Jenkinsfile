pipeline {
    agent any
    environment {
        SEMGREP_APP_TOKEN = credentials('semgrep-token') // Ensure you have the Semgrep API token stored in Jenkins credentials
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Padma-priya746/Railway-Reservation-Application.git'
            }
        }
        stage('Install Semgrep') {
            steps {
                // Install Semgrep using pip
                sh 'pip install semgrep'
            }
        }
        stage('Run Semgrep') {
            steps {
                // Run Semgrep scan
                sh 'semgrep --config auto --auth-token $SEMGREP_APP_TOKEN'
            }
        }
        stage('Archive Results') {
            steps {
                // Archive the Semgrep results
                archiveArtifacts artifacts: '**/semgrep-output.txt', allowEmptyArchive: true
            }
        }
    }
    post {
        always {
            // Publish Semgrep results
            sh 'cat semgrep-output.txt'
        }
    }
}
