pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from GitHub repository
                git branch: 'main',
                    url: 'https://github.com/iammuirurimaina/gallery.git'
            }
        }

        stage('Verify Environment') {
            steps {
                //Checking if Node.js and npm are installed
                echo 'Checking Node.js and npm versions'
                sh 'node --version'
                sh 'npm --version'
            }
        }

        stage('Install Dependencies') {
            steps {
                //Install dependencies
                echo 'Installing dependencies...'
                sh 'npm install'
            }
        }
    }
}