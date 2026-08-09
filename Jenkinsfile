@Library("Shared") _
pipeline{
    agent {label "builder"};
    stages{
        stage("Code clone"){
            steps{
                script{
                    configuration('https://github.com/Adityasinhase/two-tier-flask-app.git', "master")
                }
            }
        }
        stage("Build"){
        steps {
            // sh "docker build -t flask_app_image:latest ."
            script{
            build("flask_app_image","latest")}
        }
        }

        stage("Push to Docker hub"){
            steps{
               image_push("dockerhubcreds","flask_app_image","latest""flask_app_image","latest")
            }
        }

        stage("Execution"){
            steps{
                sh "docker compose up -d"
            }
        }
    }
    post{
        success{
            script{
                emailext from:'adicloudcraft@gmail.com',
                    subject:"Build Successful",
                    body:"Good News: Your build was successful!",
                    to:'ms2419668@gmail.com'
                    }
                }
        failure{
            script{
            emailext from:'adicloudcraft@gmail.com',
                subject:"Build failed",
                body:"Bad News:  Production failed",
                to:'ms2419668@gmail.com'
                }
            }
    }
}
