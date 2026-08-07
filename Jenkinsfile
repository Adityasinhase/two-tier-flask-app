pipeline{
    agent any;
    stages{
        stage("Code clone"){
            steps{
                git url: 'Adityasinhase/two-tier-flask-app.gitt',
                branch: "master"
            }
        }

        stage("Build"){
        steps {
            sh "docker build -t flask_app_image:latest ."
        }
        }

        stage("Push to Docker hub"){
            steps{withCredentials([usernamePassword(credentialsId:"dockerhubcreds",
                    passwordVariable: "dockerHubPassword",
                    usernameVariable: "dockerHubUsername")])
                {
                sh "docker login -u ${env.dockerHubUsername} -p ${env.dockerHubPassword}"
                sh "docker image tag flask_app_image ${env.dockerHubUsername}/flask_app_image:latest"
                sh "docker push ${env.dockerHubUsername}/flask_app_image:latest"
                }
            }
        }

        stage("Execution"){
            steps{
                sh "docker compose up -d"
            }

        }
    }
}
