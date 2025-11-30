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



        stage('Install Dependencies') {
            steps {
                // Install dependencies
                echo 'Installing dependencies...'
                sh 'npm install'
            }
        }
    }
}