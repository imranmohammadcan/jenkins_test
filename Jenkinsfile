pipeline {
    environment {
        VERSION = "${BUILD_NUMBER}"
        PROJECT = "wabapp3"
    }
    agent any
    stages {
        stage('Cloning our Git') {
            steps {
                  sh 'rm -rf dockertest1'
                   sh 'git clone https://github.com/mavrick202/dockertest1.git'        
            }
        }
        stage('Building our image') {
            steps {
                sh 'cd /var/lib/jenkins/workspace/sunny1/dockertest1'
                sh 'cp /var/lib/jenkins/workspace/sunny1/dockertest1/* /var/lib/jenkins/workspace/sunny1'
                sh 'docker build . -t imran319/sunny:v2'
            }
        }
        stage('Push Image To DockerHUB') {
            steps {
                 sh 'docker push imran319/sunny:v2'
                
            }
        }
        stage('Deploying to Docker Swarm') {
            steps {  
              sh 'docker -H tcp://172.31.29.37:2375 run --rm -dit --name webapp5 --hostname webapp5 -p 9002:80 imran319/sunny:v2'
            }
        }
        stage('Verifying The Deployment') {
            steps {
                 sh 'curl ec2-13-58-201-216.us-east-2.compute.amazonaws.com:9002' 
            }
        }
        post {
            always {
                 cleanWs()
            }
        } 
    }
}
