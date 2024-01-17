pipeline {
    agent any
    
    stages {
        stage('Clean Up') {
            steps {
                // Clean up existing containers and images
                script {
                    sh 'docker stop $(docker ps -a -q) || true'
                    sh 'docker rm $(docker ps -a -q) || true'
                    sh 'docker rmi $(docker images -q) || true'
                }
            }
        }

        stage('Setup') {
            steps {
                script {
                    // Delete temp directory if it exists
                    sh 'rm -rf temp || true'
                    
                    // Create and cd to temp directory
                    sh 'mkdir temp'
                    sh 'cd temp'
                }
            }
        }

        stage('Git Clone') {
            steps {
                // 2. Git clone repo 'aaa'
                script {
                    sh 'git clone https://github.com/Aviad-Yarkoni/DevSecOps-End-project.git'
                }
                script{
                sleep(time:60,unit:"SECONDS")
                }
            }
        }

        stage('Docker Build') {
            steps {
                // 3. Docker build
                script {
                    sh 'docker build -t end_projent .'
                }
                script{
                sleep(time:60,unit:"SECONDS")
                }
            }
        }

        stage('Docker Run') {
            steps {
                // 4. Docker run for the new image
                script {
                    sh 'docker run -d --name end_projent_test -name end_projent '
                }
                script{
                sleep(time:60,unit:"SECONDS")
                }
            }
        }

        stage('Cleanup') {
            steps {
                // Cleanup Docker images and containers
                script {
                    sh 'docker stop end_projent_test || true'
                    sh 'docker rm end_projent_test || true'
                    sh 'docker rmi end_projent || true'
                }
            }
        }
    }
}