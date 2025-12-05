pipeline {
    agent any
            tools {
            nodejs 'recent node' }

    environment {
        EMAIL_RECIPIENT = 'ian.maina@student.moringaschool.com'
        DEPLOYMENT_URL = 'https://gallery-ian.onrender.com/'
        SLACK_CHANNEL = 'ian_ip1'
    }

    stages {
        //
        stage('Checkout') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/iammuirurimaina/gallery.git'
            }
        }

        stage('Verify Environment') {
            //test node and npm version
        
            steps {
                echo 'Checking Node.js and npm versions'
                sh 'node --version'
                sh 'npm --version'
            }
        }



        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh 'npm install'
            }
        }




        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'npm test'
            }
            // post {
            //     success {
            //         emailext attachLog: true,
            //             body: """
            //                 <p>EXECUTED: Job <b>'${env.JOB_NAME}:${env.BUILD_NUMBER}'</b></p>
            //                 <p>
            //                     View console output at
            //                     <a href='${env.BUILD_URL}'>${env.JOB_NAME}:${env.BUILD_NUMBER}</a>
            //                 </p>
            //                 <p><i>(Build log is attached.)</i></p>
            //             """,
            //             subject: "Status: 'SUCCESS' - Job '${env.JOB_NAME}:${env.BUILD_NUMBER}'",
            //             to: "${env.EMAIL_RECIPIENT}"
            //     }
            //     failure {
            //         emailext attachLog: true,
            //             body: """
            //                 <p>EXECUTED: Job <b>'${env.JOB_NAME}:${env.BUILD_NUMBER}'</b></p>
            //                 <p>
            //                     View console output at
            //                     <a href='${env.BUILD_URL}'>${env.JOB_NAME}:${env.BUILD_NUMBER}</a>
            //                 </p>
            //                 <p><i>(Build log is attached.)</i></p>
            //             """,
            //             subject: "Status: FAILURE - Job '${env.JOB_NAME}:${env.BUILD_NUMBER}'",
            //             to: "${env.EMAIL_RECIPIENT}"
            //     }
            // }
        }

        stage('Deploy Verification') {
            steps {
                echo 'Checking if website is online...'
                sh "curl -I ${env.DEPLOYMENT_URL}"
                echo 'Website is live!'
            }
        }
    }

    post {
        always {
            script {
                def buildStatus = currentBuild.result ?: 'SUCCESS'
                def slackColor = 'good'
                def messageText = "Build ${env.BUILD_NUMBER} (${buildStatus}) - Live URL: ${env.DEPLOYMENT_URL}"

                if (buildStatus == 'FAILURE') {
                    slackColor = 'danger'
                    messageText = "Deployment FAILED! Build ${env.BUILD_NUMBER} (${buildStatus})"
                } else if (buildStatus == 'UNSTABLE') {
                    slackColor = 'warning'
                }

                slackSend(
                    channel: "${env.SLACK_CHANNEL}",
                    color: slackColor,
                    message: messageText
                )
            }
        }
                success {
            mail to: "${env.EMAIL_RECIPIENT}",
                 subject: "Status: 'SUCCESS' - Job '${env.JOB_NAME}:${env.BUILD_NUMBER}'",
                 body: """
                     <html>
                         <body style="font-family: Arial, sans-serif;">
                             <h2 style="color: green;">Build Successful! ✓</h2>
                             <p><b>Job Name:</b> ${env.JOB_NAME}</p>
                             <p><b>Build Number:</b> ${env.BUILD_NUMBER}</p>
                             <p><b>Build Status:</b> <span style="color: green; font-weight: bold;">SUCCESS</span></p>
                             <p><b>Deployment URL:</b> <a href="${env.DEPLOYMENT_URL}">${env.DEPLOYMENT_URL}</a></p>
                             <p><a href="${env.BUILD_URL}">View Console Output</a></p>
                         </body>
                     </html>
                 """
        }
        failure {
            mail to: "${env.EMAIL_RECIPIENT}",
                 subject: "Status: FAILURE - Job '${env.JOB_NAME}:${env.BUILD_NUMBER}'",
                 body: """
                     <html>
                         <body style="font-family: Arial, sans-serif;">
                             <h2 style="color: red;">Build Failed! ✗</h2>
                             <p><b>Job Name:</b> ${env.JOB_NAME}</p>
                             <p><b>Build Number:</b> ${env.BUILD_NUMBER}</p>
                             <p><b>Build Status:</b> <span style="color: red; font-weight: bold;">FAILURE</span></p>
                             <p><b>Deployment URL:</b> <a href="${env.DEPLOYMENT_URL}">${env.DEPLOYMENT_URL}</a></p>
                             <p><a href="${env.BUILD_URL}">View Console Output</a></p>
                         </body>
                     </html>
                 """
        }
    }
}

