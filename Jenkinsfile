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
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker tag node-app-test-new marseloffl/todo-node-app:1.0"
                    sh "docker push marseloffl/todo-node-app:1.0" 
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
