@Library("shared") _
pipeline {
    agent { label "jenkins" }
    
    stages{
        stage("hello"){
            steps{
                script{
                    hello()
                    hello()
                }
            }
        }
        stage("code"){
            steps{
                echo "this is cloning the code"
               script{
                clone("https://github.com/wadood786/django-notes-app.git","main")
            }
                echo "Code cloned successfully"
        }
        }
        
        stage("build"){
            steps{
                echo "this is building the code"
               script{
               docker_build("notes-app","latest","abdulwadood786")
            }
                echo "image created successfully"            
          }
        }
        stage("Push to Dockerhub"){
            steps{ 
                echo "Imsges is in push state"
                script{
                docker_push("notes-app","latest","abdulwadood786")
                }
                echo "image pushed successfully"
            }
        }
        stage("deploy"){
            steps{ 
                echo "code has deployed"
                sh "docker compose up -d"
                echo "deployed successfully"
            }
        }
    }
}
