pipeline {
    agent {
        docker{
            image 'node:14.8.0-alpine'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Instal deps'){
            steps{
                echo 'Installing dependencies'
                sh 'npm install'
            }
        }
        stage('Run tests'){
            steps{
                echo 'Running tests'
                sh 'npm test'
            }
        }
    }
}
