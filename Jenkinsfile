pipeline {
    agent any
    
    stages{
        stage("Code"){
            steps{
                git url: "https://github.com/Bakhtawarkhan90/two-tier-app.git", branch: "main"
            }
        }
        stage("Build "){
            steps{
                sh "docker build . -t flaskapp"
            }
        }
        stage("Push to DockerHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker tag flaskapp ${env.dockerHubUser}/flaskapp:latest"
                    sh "docker push ${env.dockerHubUser}/flaskapp:latest" 
                }
            }
        }
        stage("Deploy"){
            steps{
                sh "docker compose down"  
                sh "docker compose up -d"
            }
        }
    }
}
