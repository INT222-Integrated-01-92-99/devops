pipeline {
    agent any

    stages {

        stage('(stop), remove container and image') {
            steps {
                script {
                    def haveImg = sh(script: 'docker images -q frontend', returnStdout: true) == ""
                    println haveImg

                    if( !haveImg ){
                           sh 'docker stop ppclothesFE'
                           sh 'docker rm ppclothesFE'
                           sh 'docker image rm frontend'
                    }else {
                        echo 'Skip this stage '
                    }
                }
            }
        }

        stage('remove whole data in workspace') {
            steps {
                sh 'rm -rf *'
            }
        }

        stage('git clone') {
            steps {
                git branch: 'master',
                    credentialsId: 'jenkinsid',
                    url: 'https://github.com/INT222-Integrated-01-92-99/frontend.git'
            }
        }

        stage('(deploy) start container') {
            steps {
                sh 'docker-compose up -d'
            }
        }

    }
}