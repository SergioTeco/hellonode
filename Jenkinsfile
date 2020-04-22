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
                    docker.withRegistry('https://registry.hub.docker.com', '4bdd8687-8b57-454d-b3c6-123d51ed09d4') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
        stage('DeployToProduction') {	
            steps {	
                milestone(1)	
                kubernetesDeploy(	
                    kubeconfigId: '7b103d5e-25ef-4057-9282-d876711cd976',	
                    configs: 'k8s_svc_deploy.yaml',	
                    enableConfigSubstitution: true	
                )	
            }	
        }
    }
}
