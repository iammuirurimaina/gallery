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

        stage('Deploy to Render') {
            steps {
                echo 'Deploying to Render...'
                
                // Check if website is online
                echo 'Checking if website is online...'
                sh 'curl -I https://gallery-ian.onrender.com/'
                echo 'Website is live!'
            }
        }
    }
}