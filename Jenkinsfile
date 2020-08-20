pipeline {
    agent any
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
        stage('Zip file'){
            steps{
                echo 'Zipping files'
                sh 'zip content.zip -r .'
                sh 'scp content.zip nodejs@10.0.1.20/home/'
            }
        }
    }
}
