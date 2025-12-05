pipeline {
    agent any

    stages {

        stage ("clone repo") {
            steps {
                git branch: 'main', url: 'https://github.com/iammuirurimaina/gallery.git'}
        }
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'npm install'
                sh 'npm run build'
            }
        }
        // stage('Test') {
        //     steps {
        //         echo 'Testing...'
        //     }
        // }
        // stage('Deploy') {
        //     steps {
        //         echo 'Deploying...'
        //     }
        // }
    }


}
