pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing npm dependencies...'
                bat 'npm install'      
                bat 'npm --version || true'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                bat 'npm run test'
            }
        }

        stage('Archive Artifact') {
            steps {
                echo 'Archiving build output...'
                bat 'tar -a -c -f build-artifact.zip index.js package.json'
                archiveArtifacts artifacts: 'build-artifact.zip', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Build completed'
        }
        failure {
            echo 'Build failed.'
        }
    }
}
