pipeline {
    agent any
    stages {
        stage('Instal deps'){
            steps{
                echo 'Installing dependencies'
                sh 'rm -rf *.tar.gz'
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
                sh 'tar czf content-$BUILD_NUMBER.tar.gz server.js package.json test.js Dockerfile Jenikinsfile .dockerignore'
                sh 'scp content-$BUILD_NUMBER.tar.gz nodejs@10.0.1.20/home/'
            }
        }
        stage('Build and run'){
            steps{
                sh 'ssh nodejs@10.0.1.20 docker build -t nodejschallenge:latest - < content-$BUILD_NAME.tar.gz'
                sh 'ssh nodejs@10.0.1.20 docker run -p 8000:8000 nodejschallenge:latest'
            }
        }
    }
}
