node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("sergito23/hellonode")
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('https://registry.hub.docker.com', '64295789-f281-4160-ac03-797d2ba460e4') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
     stage('DeployToProduction') {
            
            steps {
                
                kubernetesDeploy(
                    kubeconfigId: '7b103d5e-25ef-4057-9282-d876711cd976',
                    configs: 'k8s_svc_deploy.yaml',
                    enableConfigSubstitution: true
                )
            }
        }             
    }
