pipeline {
    agent any
    stages {
        stage('start') {
            steps {
              echo 'salut monsieur!'
              echo 'test is doker running'
              sh 'docker ps'

            }
        }
        stage('build') {
            steps {
              echo 'build docker image'
              sh 'docker build -t iotimage .'
            }
        }
        stage('push'){
            steps {
                echo 'pushing to docker hub'
                withCredentials([usernamePassword(credentialsId: 'dockerhubcred', usernameVariable: 'DOCKERHUB_LOGIN', passwordVariable: 'DOCKERHUB_PASS')]) {
                        sh '''
                            echo $DOCKERHUB_PASS | docker login --username $DOCKERHUB_LOGIN --password-stdin
                            docker image tag iotimage $DOCKERHUB_LOGIN/iotimage:16
                            docker image push $DOCKERHUB_LOGIN/iotimage:16
                        '''
                        }
            }
        }

    }
}