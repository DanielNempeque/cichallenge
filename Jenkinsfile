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
                sh 'ls -a'
                sh 'pwd'
                sshagent(['ssh-key-1']) {
                    sh 'scp -i key.pem content-$BUILD_NUMBER.tar.gz vagrant@10.0.1.20:/home/vagrant'
                }  
            }
        }
        stage('Build and run'){

            steps{
                sshagent(['ssh-key-1']) {
                    sh 'ssh -i key.pem vagrant@10.0.1.20 sudo docker build -t nodejschallenge:latest - < content-$BUILD_NUMBER.tar.gz'
                    sh 'ssh -i key.pem vagrant@10.0.1.20 sudo docker run -p 8000:8000 -d nodejschallenge:latest --name challenge'
                }   
            }
        }
    }
}
