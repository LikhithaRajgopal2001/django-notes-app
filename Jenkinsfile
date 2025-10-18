pipeline{
    agent { label "Agent"}
    
    stages{
        stage("Code"){
        steps{
            echo "Cloning the code"
            git url: "https://github.com/LondheShubham153/django-notes-app.git", branch:"main"
            echo "code cloned successfully"
        }
    }
    stage("Build"){
        steps{
            echo " Building"
            sh "docker build -t notes-app:latest ."
        }
    }
    stage("push to Docker hub"){
        steps{
             echo " Pushing image to docker hub"
             withCredentials([usernamePassword(
                 'credentialsId':"dockerhubcred", 
                 passwordVariable: "dockerhubpass",
                 usernameVariable: "dockerhubuser")])
             sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass} "
             sh "docker image tag notes-app:latest ${env.dockerhubuser}/notes-app:latest"
             sh "docker push ${env.dockerhubuser}/notes-app:latest"
             
        }
    }
    stage("Deploy"){
        steps{
             echo " Deploying"
             sh "docker compose up -d"
        }
    }
    }
}
