pipeline {
    agent any
    
    stages {
        
        stage("code"){
            steps{
                git url: "https://github.com/Hritik1706/node-todo-app", branch: "main"
                echo 'clone successfull'
            }
        }
        stage("build and test"){
            steps{
                sh "docker build -t hritik1706/node-todo-app:lts ."
                echo 'buildcsuccessfull '
            }
        }
        stage("push"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/node-todo-app:lts"
                echo 'image push successfull'
                }
            }
        }
        stage("deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
                echo 'deployment successfull'
            }
        }
    }
}
