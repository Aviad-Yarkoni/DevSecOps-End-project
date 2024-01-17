pipeline {
  agent any
  environment {
        APP_IMAGE = 'shmuela6/tasksapp:12.1'
        UNIT_TEST_IMAGE = 'shmuela6/tasksapp:test_unit_updated'
        INT_TEST_IMAGE = 'shmuela6/tasksapp:tests_latest'
    }
  stages {

    stage('Run Unit Test'){
        steps{
            echo 'Start unit test'
            sh "docker run ${env.UNIT_TEST_IMAGE}"
            script{
                sleep(time:5,unit:"SECONDS")
            }
        }
    }

    stage('Run Tasks App'){
        steps{
            echo 'Start app'
            sh "docker run -d -p 80:5000 ${env.APP_IMAGE}"
            script{
                sleep(time:10,unit:"SECONDS")
            }
        }
    }

    stage('Run Integration Test'){
        steps{
            echo 'Start integration test'
            sh "docker run --platform linux/amd64 ${env.INT_TEST_IMAGE}"
        }
    }


    
    stage('Clean resources'){
        steps{
            echo 'Stopping containers'
            sh '''docker stop $(docker ps -a -q)'''
            echo 'Removing containers'
            sh '''docker rm $(docker ps -a -q)'''
        }
    }
  }
  post{
    success {
        echo 'Unit and integration test ran successfully.'
    }
    failure{
        echo 'Unit and integration test failed.'
    }
  }

}