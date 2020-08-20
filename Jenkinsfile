pipeline {
    agent any
    tools {nodejs "NodeJs"}
    stages {
        stage('Instal deps'){
            steps{
                echo 'Installing dependencies'

                nodejs()
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
