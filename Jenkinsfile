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
                    docker.withRegistry('https://registry.hub.docker.com', '5e502a09-1e43-49c9-9d5e-d0c7d7259578') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
       
    }
}
