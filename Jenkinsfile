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
                    docker.withRegistry('https://registry.hub.docker.com', '9c64bb22-55a0-455e-b256-079f01b3d3bc') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
        
    }
}
