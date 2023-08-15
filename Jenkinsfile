pipeline {
    agent { label 'dev-node' }
    stages{
        stage('Code Build'){
            steps{
                git url: 'https://github.com/dheeraj001/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('Build'){
            steps{
               sh 'docker build . -t devopslove/node-todo-app-cicd:latest'
            }
        }
        stage('login and push image'){
            steps{
               withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerhubpasswd', usernameVariable: 'dockerhubuser')]){
                   sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpasswd}"
                   sh "docker push devopslove/node-todo-app-cicd:latest"
               }
                   
            }
        }
        stage('Deploy'){
            steps{
               sh 'docker-compose down && docker-compose up -d'
            }
        }
        
        
    }
    
}
