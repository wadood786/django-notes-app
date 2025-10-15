@Library('Shared') _
pipeline{
    agent any
    
    stages{
        stage("Code clone"){
            steps{
                sh "whoami"
            cloning("https://github.com/abdulwadood786/django-notes-app.git","main")
            }
        }

        stage("trivy File system scanning"){
            steps{
                script{
                    trivy_scan()
                }
            }
            
        }
        
        stage("Code Build"){
            steps{
            docker_building("notes-app","latest", "abdulwadood786")
            }
        }
        stage("Push to DockerHub"){
            steps{
                docker_pushing("abdulwadood786","notes-app","latest")
            }
        }
        stage("Deploy"){
            steps{
                echo "App is ready to deploy"
                sh "docker compose up -d"
                echo "app has deployed"
            }
        }
        
    }
}
