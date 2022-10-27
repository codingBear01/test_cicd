pipeline{
    agent any
    tools {
      nodejs "node 16.18.0"
      git "git"
    }
    options {
        skipStagesAfterUnstable()
    }
    environment {
        ECR_REPO = "347222812711.dkr.ecr.ap-northeast-2.amazonaws.com/test_cicd"
        AWS_CREDENTIALS="ID_DEPLOY_USER"
        GIT_CREDENTIAL_ID = "fe_test_account"
        NAME = "test_cicd"
        GIT_URL="https://github.com/codingBear01/test_cicd"
    }
    stages {
          stage('Clone repository') { 
            steps { 
                script{
                checkout scm
                }
            }
        }
        stage('Build') { 
            steps { 
                script{
                  app = docker.build("${NAME}")
                }
            }
        }
        stage('Test'){
            steps {
                  echo 'Empty'
            }
        }
        stage('Deploy') {
            steps {
                script{
                        docker.withRegistry("https://${ECR_REPO}", "ecr:us-east-2:${AWS_CREDENTIALS}") {
                    app.push("${env.BUILD_NUMBER}")
                    app.push("latest")
                    }
                }
            }
        }
    }
}