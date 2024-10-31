@Library("Shared") _
pipeline{
    agent {label "agent1"}
    
 

    stages {
        
        stage('Hello') {
            steps{
                script{
                    hello()
                }
            }
                
        }
        stage('code') {
            steps {
                echo 'cloning the code'
                script{
                    clone("https://github.com/gauravsewatkar/django-notes-app.git", "main")
                }
 
                echo "code cloned successfully"
            }
        }
        
    stage('build') {
            steps {
                echo 'The build is ongoing'
                script{
                    docker_build("notes-app", "latest", "garry1325")
                }
                //sh "docker build -t notes-app:latest ."
                echo 'The build is done'
            }
        }
        
    stage('test') {
            steps {
                echo 'Hello World'
            }
        }  
        
    stage('Push to Dockerhub') {
            steps {
                echo "Pushing image to dockerhub"
                script{
                    docker_push("notes-app", "latest", "garry1325")
                }
                // withCredentials([usernamePassword(credentialsId:"dockerhub-cred",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                // sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                // sh "docker image tag notes-app:latest ${env.dockerHubUser}/notes-app:latest"
                // sh " docker push ${env.dockerHubUser}/notes-app:latest "
                }
            }
    stage('deploy') {
            steps {
                echo "deploying the code"
                sh "docker compose up -d"
            }
        }            
    }        
    
    
}


