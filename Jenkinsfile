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
        stage("Build"){
            steps{
                sh "docker build -t marseloffl/todo-node-app:1.0 ."
            }
        }
        stage("Login"){
            steps{
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push') {
      steps {
        sh "docker push marseloffl/todo-node-app:1.0"
      }
    }
        stage('Deploy') {
            steps 
			{
                sh "docker run -d --name toto-app -p 8000:8000 marseloffl/todo-node-app:1.0"
            }
        }
        //stage("Deploy"){
          //  steps{
            //    sh "docker-compose down && docker-compose up -d"
            //}
        //}
    }
}
