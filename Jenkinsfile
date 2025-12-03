pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'ian.maina@student.moringaschool.com'
    }

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
                success {
                    emailext attachLog: true,
                        body: """
                            <p>EXECUTED: Job <b>'${env.JOB_NAME}:${env.BUILD_NUMBER}'</b></p>
                            <p>
                                View console output at
                                <a href='${env.BUILD_URL}'>${env.JOB_NAME}:${env.BUILD_NUMBER}</a>
                            </p>
                            <p><i>(Build log is attached.)</i></p>
                        """,
                        subject: "Status: 'SUCCESS' - Job '${env.JOB_NAME}:${env.BUILD_NUMBER}'",
                        to: "${env.EMAIL_RECIPIENT}"
                }
                failure {
                    emailext attachLog: true,
                        body: """
                            <p>EXECUTED: Job <b>'${env.JOB_NAME}:${env.BUILD_NUMBER}'</b></p>
                            <p>
                                View console output at
                                <a href='${env.BUILD_URL}'>${env.JOB_NAME}:${env.BUILD_NUMBER}</a>
                            </p>
                            <p><i>(Build log is attached.)</i></p>
                        """,
                        subject: "Status: FAILURE - Job '${env.JOB_NAME}:${env.BUILD_NUMBER}'",
                        to: "${env.EMAIL_RECIPIENT}"
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

        }
    }
post {
        //post to slck channel after every build
        always {
            def buildStatus = currentBuild.result
            def slackColor = 'good'
            def messageText = "Build ${env.BUILD_NUMBER} (${buildStatus}) - Live URL: https://gallery-ian.onrender.com/"

            if (buildStatus == 'FAILURE') {
                slackColor = 'danger'
                messageText = "Deployment FAILED! Build ${env.BUILD_NUMBER} (${buildStatus})"
            } else if (buildStatus == 'UNSTABLE') {
                slackColor = 'warning'
            }

            slackSend(
                channel: 'ian_ip1',
                color: slackColor,
                message: messageText
            )
        }
    }
}