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
                    sh 'DOCKER_BUILDKIT=0 docker build . -t endprojent:one'
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
                    sh 'docker run -d --name test_end_project -p 9090:8000 endprojent:one '
                }
                script{
                sleep(time:60,unit:"SECONDS")
                }
            }
        }

        stage('Check Response') {
            steps {
                // Check response from 127.0.0.1:909
                script {
                    def response = sh(script: 'curl -s -o /dev/null -w "%{http_code}" http://127.0.0.1:909', returnStatus: true).trim()
                    echo "HTTP Response Code: ${response}"
                    
                    if (response == '200') {
                        echo "Successfully received a 200 OK response."
                    } else {
                        error "Failed to receive a 200 OK response."
                    }
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
                    sh 'cd /var/jenkins_home/workspace/'
                    sh 'rm -rf *'
                }
            }
        }
    }
}