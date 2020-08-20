pipeline {
    agent any
    tools (nodejs "node")
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
