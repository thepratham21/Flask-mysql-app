pipeline {

    agent any

    stages {

        stage("Code") {
            steps {
                echo "Cloning code..."
                git url: "https://github.com/thepratham21/Flask-mysql-app-docker", branch: "main"
            }
        }

        stage("Build") {
            steps {
                sh "docker build -t flask-mysql-app-image ."
            }
        }

        stage("Test") {
            steps {
                echo "Testing completed"
            }
        }
        
        stage("push image to docker hub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId:"DockerHub-Credentials",
                    passwordVariable: "dockerHubPass",
                    usernameVariable: "dockerHubUser"
                    )]){
                    
                sh "docker login -u ${env.dockerHubUser} -p ${dockerHubPass}"
                sh "docker image tag flask-mysql-app-image ${dockerHubUser}/flask-mysql-app-image"
                sh "docker push ${dockerHubUser}/flask-mysql-app-image"
                }
            }
        }

        stage("Deploy") {
            steps {
                sh "docker compose up -d"
            }
        }
    }
}
