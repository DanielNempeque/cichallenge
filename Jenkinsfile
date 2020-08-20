pipeline {
    agent any
    stages {
        stage('Instal deps'){
            steps{
                echo 'Installing dependencies'
                sh 'node -v'
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
