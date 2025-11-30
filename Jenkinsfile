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

        stage('Test') {
                //run tests and send email incase 1 fails
            steps {
                echo 'Running tests...'
                sh 'npm test'
            }
            post {
                failure {
                    echo 'Tests failed! Sending email notification...'
                    mail to: 'ian.maina@student.moringaschool.com',
                         subject: "Test Failed"
                }
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
            post {
                success {
                    
                    slackSend(
                        color: 'good',
                        message: "Deployment Successful! Build ID: ${env.BUILD_ID}\nLive URL: https://gallery-ian.onrender.com/"
                    )
                }
        }
    }
}