pipeline {
    agent any
    
    stages {
        stage('Setup') {
            steps {
                script {
                    // 1. Make directory 'temp' and cd to temp
                    dir('temp') {
                        sh 'mkdir temp'
                        sh 'cd temp'
                    }
                }
            }
        }

        stage('Git Clone') {
            steps {
                // 2. Git clone repo 'aaa'
                script {
                    sh 'git clone https://github.com/Aviad-Yarkoni/DevSecOps-End-project.git'
                }
            }
        }

         stage('Sleep') {
            steps {
                // Introduce a 60-second sleep
                sh 'sleep 60'
            }
        }

        stage('Docker Build') {
            steps {
                // 3. Docker build
                script {
                    sh 'docker build -t end_projent .'
                }
            }
        }

         stage('Sleep') {
            steps {
                // Introduce a 60-second sleep
                sh 'sleep 60'
            }
        }

        stage('Docker Run') {
            steps {
                // 4. Docker run for the new image
                script {
                    sh 'docker run -d --name end_projent_test -name end_projent '
                }
            }
        }

         stage('Sleep') {
            steps {
                // Introduce a 60-second sleep
                sh 'sleep 60'
            }
        }
        stage('Cleanup') {
            steps {
                // Cleanup Docker images and containers
                script {
                    sh 'docker stop your-container-name || true'
                    sh 'docker rm your-container-name || true'
                    sh 'docker rmi your-image-name || true'
                }
            }
        }
    }
}