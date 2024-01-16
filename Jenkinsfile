pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    // Clean up workspace before cloning
                    deleteDir()

                    // Clone the GitHub repository
                    git branch: 'main', url: 'https://github.com/Aviad-Yarkoni/DevSecOps-End-project'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image using the Dockerfile in the repository
                    docker.build("my-docker-image:${env.BUILD_NUMBER}")
                }
            }
        }

        stage('Run Docker Image') {
            steps {
                script {
                    // Run the Docker image
                    docker.image("my-docker-image:${env.BUILD_NUMBER}").run()
                }
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    // Stop and remove running containers
                    sh 'docker ps -aq | xargs docker stop'
                    sh 'docker ps -aq | xargs docker rm'

                    // Remove Docker images
                    sh 'docker images -q | xargs docker rmi'
                }
            }
        }
    }

    post {
        always {
            // Clean up workspace after pipeline execution
            deleteDir()
        }
    }
}
