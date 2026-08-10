@Library("Shared") _
pipeline{
    agent {label "builder"};
    stages{
        stage("Code clone"){
            steps{
                script{
                    configuration('https://github.com/Adityalsinhase/two-tier-flask-app.git', "master")
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
                script{
               image_push("dockerhubcreds","flask_app_image","latest")
                }
                }
        }

        stage("Execution"){
            steps{
                script{
                    execute()
                }
            }
        }
    }
    post{
        success{
            script{
                result("adicloudcraft@gmail.com","Build Successful","Good News: Your build was successful!","ms2419668@gmail.com")
                    }
                }
        failure{
            script{
                result("adicloudcraft@gmail.com","Build Faliure","Bad News: Your build was failed Need your immidiate attention","ms2419668@gmail.com")
                }
            }
    }
}
