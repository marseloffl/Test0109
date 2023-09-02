pipeline {
    agent any
    
    stages{
        stage("Code"){
            steps{
                git url: "https://github.com/marseloffl/test0109.git", branch: "master"
            }
        }
        stage("Build & Test"){
            steps{
                sh "docker build -t marseloffl/todo-node-app:1.0 ."
            }
        }
        stage("Push to DockerHub"){
            steps{
withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                    sh "docker tag node-app-test-new ${env.dockerHubUser}/todo-node-app:1.0"
                    sh "docker push ${env.dockerHubUser}/todo-node-app:1.0" 
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
