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
                sh 'tar czf content-$BUILD_NUMBER.tar.gz server.js package.json test.js Dockerfile Jenkinsfile'
                sh 'scp content-$BUILD_NUMBER.tar.gz nodejs@10.0.1.20'
            }
        }
        stage('Build and run'){
            steps{
                sh 'ssh -oStrictHostKeyChecking=no nodejs@10.0.1.20 docker build -t nodejschallenge:latest .'
                sh 'ssh -oStrictHostKeyChecking=no nodejs@10.0.1.20 docker run -p 8000:8000 -d nodejschallenge:latest --name challenge'
            }
        }
    }
}
