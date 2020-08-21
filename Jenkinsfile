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
                sshagent(credentials: ['ssh-key-1']) {
                    sh 'scp -o StrictHostKeyChecking=no content-$BUILD_NUMBER.tar.gz vagrant@10.0.1.20:/home/vagrant'
                }  
            }
        }
        stage('Build and run'){
            steps{
                echo 'Building docker image'
                sshagent(credentials: ['ssh-key-1']) {
                    sh 'ssh -o StrictHostKeyChecking=no vagrant@10.0.1.20 sudo docker build -t nodejschallenge:latest - < content-$BUILD_NUMBER.tar.gz'
                    sh 'ssh -o StrictHostKeyChecking=no vagrant@10.0.1.20 sudo docker stop challenge || true && docker rm challenge || true'
                    sh 'ssh -o StrictHostKeyChecking=no vagrant@10.0.1.20 sudo docker run -p 8000:8000 -d --name challenge nodejschallenge:latest'
                }   
            }
        }
    }
}
