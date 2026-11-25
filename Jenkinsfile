pipeline{
    agent { label 'worker'}
    
    stages{
        stage("Code clone"){
            steps{
                echo "cloning code"
                sh "whoami"
                git url: "https://github.com/kruthijan25-hash/django-notes-app.git", branch: "main"
                echo "sucess"
            }
        }
        stage("Code Build"){
            steps{
                 echo "Build"
                 sh "docker build -t notes-app:latest ."
                 
            }
        }
        stage("Push to DockerHub"){
            steps{
                echo "push"
                withCredentials([usernamePassword(
                        credentialsId: 'dockerHubCred',
                        usernameVariable: 'DOCKERUSER',
                        passwordVariable: 'DOCKERPASS'
                    )]){
                sh "docker login -u ${env.DOCKERUSER} -p ${env.DOCKERPASS}"
                sh "docker image tag notes-app:latest ${env.DOCKERUSER}/notes-app.latest"
                sh "docker push ${env.DOCKERUSER}/notes-app.latest"
                }
            }
        }
    
        stage(" Docker container"){
            steps{
                echo "push"
                sh "docker compose down && docker compose up -d"
               
            }
        }
        
    }
}
