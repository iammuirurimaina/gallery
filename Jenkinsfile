pipeline {
    agent any
    // Define the email recipient

    environment {
        EMAIL_RECIPIENT = 'ian.maina@student.moringaschool.com'
        DEPLOYMENT_URL = 'https://gallery-ian.onrender.com/'
        SLACK_CHANNEL = 'ian_ip1'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from GitHub repository
                git branch: 'master',
                    url: 'https://github.com/iammuirurimaina/gallery.git'
            }
@@ -23,16 +23,19 @@ pipeline {
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
@@ -64,28 +67,24 @@ pipeline {
                        subject: "Status: FAILURE - Job '${env.JOB_NAME}:${env.BUILD_NUMBER}'",
                        to: "${env.EMAIL_RECIPIENT}"
                }
            }            
            }
        }

        stage('Deploy to Render') {
        stage('Deploy Verification') {
            steps {
                echo 'Deploying to Render...'
                
                // Check if website is online 
                echo 'Checking if website is online...'
                sh 'curl -I https://gallery-ian.onrender.com/'
                sh "curl -I ${env.DEPLOYMENT_URL}"
                echo 'Website is live!'
            }

        }
    }

    post {
        //post to slack channel
        always {
            script {
                def buildStatus = currentBuild.result
                def buildStatus = currentBuild.result ?: 'SUCCESS'
                def slackColor = 'good'
                def messageText = "Build ${env.BUILD_NUMBER} (${buildStatus}) - Live URL: https://gallery-ian.onrender.com/"
                def messageText = "Build ${env.BUILD_NUMBER} (${buildStatus}) - Live URL: ${env.DEPLOYMENT_URL}"

                if (buildStatus == 'FAILURE') {
                    slackColor = 'danger'
@@ -95,11 +94,11 @@ pipeline {
                }

                slackSend(
                    channel: 'ian_ip1',
                    channel: "${env.SLACK_CHANNEL}",
                    color: slackColor,
                    message: messageText
                )
            }
        }
    }
}
}