pipeline {
    agent any
    environment {
        //be sure to replace "felipelujan" with your own Docker Hub username
        //changesss
        DOCKER_IMAGE_NAME = "sergito23/hellonode"
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    app = docker.build(DOCKER_IMAGE_NAME)
                }
            }
        }
        
        

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
        //stage('Deploy') {
           //steps {
                //sh 'docker run sergito23/hellonode , sleep 30'
                //sh 'docker stop sergito23/hellonode'
            //}
        //}   
    }
}
