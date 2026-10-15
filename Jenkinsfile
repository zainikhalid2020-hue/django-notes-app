@Library("Shared") _
pipeline{
    
    agent { label "vinod" }
    
    stages{
        stage("Hello"){
            steps{
                script{
                    hello()
                }
            }
        }
        stage("Code"){
            steps{
                script{
                    clone("https://github.com/zainikhalid2020-hue/django-notes-app.git","main")
                }
            }
        }
        stage("Build"){
            steps{
                script{
                    docker_build("notes-app","latest","saraaaa97")
                }
            }
        }
        stage("Test"){
            steps{
                echo "This is testing the code"
            }
        }
        stage("Push to DockerHub"){
            steps{
                echo "This is pushing the image to Docker Hub"
                withCredentials([usernamePassword('credentialsId':"dockerHubCred",
                passwordVariable:"dockerHubPass",usernameVariable:"docekrHubUser")]){
                sh "docker login -u ${env.docekrHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag notes-app:latest ${env.docekrHubUser}/notes-app:latest"
                sh "docker push ${env.docekrHubUser}/notes-app:latest"
                }
            }
        }
        stage("Deploy"){
            steps{
                echo "This is deploying the code"
                sh "docker compose down && docker compose up -d"
            }
        }
    }
}
