@Library("shared_lib") _
pipeline {
    agent {
        label 'Agent1'
        }
    stages {
        stage("greeting"){
            steps {
                script {
                    hello()
                }
            }
        }
        stage("Clone code") {
          steps {
              script {
              /* echo "this is cloning the code"
                 git url:"https://github.com/Vleena/django-notes-app.git", branch:"main"
                 echo "Code cloned successfully"  */
               clone("https://github.com/Vleena/django-notes-app.git","main")
           } 
        }
        }
        stage("Build") {
            steps {
             /* echo "Building the code" 
              sh "whoami"
              sh "docker build -t django-app:latest ." */
              script {
                  docker_build("django-app","latest","vleena")
              }
           }  
        }
        stage("Test") {
             steps {
               echo "Testing the code"
           } 
        }
        stage("Push the code"){
            steps {
               /* echo "Pushing the code to the dockerhub"
                 withCredentials([usernamePassword('credentialsId':"DockerHubCred",
                passwordVariable:"DockerHubPass",
                usernameVariable:"DockerHubname")]){
                sh "docker login -u ${env.DockerHubname} -p ${env.DockerHubPass}"
                sh "docker image tag django-app:latest ${env.DockerHubname}/django-app:latest"
                sh "docker push ${env.DockerHubname}/django-app:latest" */
                script {
                    docker_push("django-app","latest","vleena")
                }
            
            }
        }
        stage("Deploy"){
             steps {
               echo "Deploying the application"
              // sh "docker run -d -p 8000:8000 django-app:latest"
              // sh "docker compose up -d"
              script{
                   deploy()
              }
           } 
        }
    }
}
