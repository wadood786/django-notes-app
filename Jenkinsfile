@Library('Shared') _ 
pipeline {
    agent any
    
    stages {
        stage("Code clone") {
            steps {
                sh "whoami"
                script {
                    cloning("https://github.com/wadood786/django-notes-app.git", "main")
                }
            }
        }

        stage("Trivy File System Scanning") {
            steps {
                script {
                    trivy_scan()
                }
            }
        }
        
        stage("Code Build") {
            steps {
                script {
                    docker_building("notes-app", "latest", "abdulwadood786")
                }
            }
        }

        stage("Push to DockerHub") {
            steps {
                script {
                    docker_pushing("abdulwadood786", "notes-app", "latest")
                }
            }
        }

        stage("Pre-Deploy Cleanup") {
            steps {
                echo "🧹 Cleaning old MySQL data..."
                sh '''
                    sudo rm -rf ./data/mysql/db || true
                    sudo mkdir -p ./data/mysql/db
                    sudo chown -R 999:999 ./data/mysql/db
                '''
            }
        }

        stage("Deploy") {
            steps {
                echo "🚀 Deploying the app..."
                sh '''
                    docker compose down -v || true
                    docker compose up -d --build
                '''
                echo "✅ App has been deployed successfully."
            }
        }
    }
}
