pipeline {
    agent any
    environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerHub')
  }
    
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
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                    sh "docker tag node-app-test-new marseloffl/todo-node-app:1.0"
            }
        }
        stage('Push') {
      steps {
        sh "docker push marseloffl/todo-node-app:1.0"
      }
    }
        //stage("Deploy"){
          //  steps{
            //    sh "docker-compose down && docker-compose up -d"
            //}
        //}
    }
}
