pipeline{
    agent any
    tools {
      nodejs "node 16.18.0"
      git "git"
    }
    environment {
        ECR_REPO = "347222812711.dkr.ecr.ap-northeast-2.amazonaws.com/test_cicd"
        AWS_CREDENTIALS="ID_DEPLOY_USER"
        GIT_CREDENTIAL_ID = "fe_test_account"
        NAME = "test_cicd"
        GIT_URL="https://github.com/codingBear01/test_cicd"
    }
    stages {
        stage('Pull') {
            steps {
                git url:"${GIT_URL}", branch:"main", 
                poll:true, 
                changelog:true, 
                credentialsId: "${GIT_CREDENTIAL_ID}"
            }
        }
        stage('Build') {
            steps {
                sh "docker build -t ${NAME} ."
                sh "docker tag ${NAME}:latest ${NAME}:latest"
            }
        }
        stage('ECR Upload'){
            steps {
                script{
                    try{
                      // withAWS(credentials:"${AWS_CREDENTIALS}", 
                      // // role: 'arn:aws:iam::347222812711:user/deploy_user', roleAccount: 'deploy_user', externalId:'externalId'
                      // ){
                        sh "aws ecr --region ap-northeast-2 | docker login -u AWS -p eyJwYXlsb2FkIjoiVlI2cElQbkkyRTV5UWhwd2Q1VWt3VHpiV3NSTWxNdDVSWUJmK0sweFFNYi95akdrcmpzNk5xOGVsMFphV0dUZE1pRFhYL25mNDd3YlFWcUhMN3BtTHdBUENCRHpUZmxWWW9JcC9ybFRhWWNxM05KS09QcHJwLzdLYVNNMzZaZFFwMEI5VCtHeWFDUjZyT3ZkVDhoRkVpcmFMb1NRSXFvNDBXdXhjMHJKVHNocWRzLzBhOE1mSmN5alp6K3JiZFEyYmkzZ2RrQ2RiRzVQSmcxNXE1WWd1YkloSzMzQUlNK3MvYlNVVER2elJJbytKb2NiQlZ0NHFES0pvTVdhL3N3SnBPM29CLzNiV1dPRldoTnVxVElWRk54VWxvM0RMRU9KSHlLM1AxakwvWkdYcDdwYVdOU3FJeW1tWEVWSWUvK0w3cVVWbG9YMzk1RmNLRVRkeSs1TlEvem9GVHdua3JDaG9IcXZiZHFpY2FqWW11SU5yZTlyZklIUFgvTUg2NlMyY0srbGZPdVp5MUgzUG5xN2thMkRaSllCcGF5TFl5REFueEQ4a0Zra002YjhHcHdZUWVwNGU0QlNLUkRvVmFsNDVqVWpjbEVPOEpPZHZzZEpRTmkzUFBPZjYycTJqQUk4dGVsVXNZT2pBVlVrTDMyaUdOUFlxR2NqbC9vNW1TWTJUTXpkbm1reVkvS29YbHRzN2NGS3dMYmEwbzJKVWkwUEhEMUtVRFY2dk5XZm1LT2hDU1BoOW9tQU5OMWdwT2FBa3U2TkRXcE5jcmdERVBxS0o3TENaaVhNZjRTdWkwQmxINjlVME9oWnpVUGZuejVsSnRVL1JCYlNLUU1uWGxPcHVIMjNqNFUyMFI4K0hEK1k4UnZabEc2aXl1azJVdm45aWlxWnIxUHFkS05QQXNrdHJ5QTJLU2JBUWZVWHR6Z0M1ejZhN0VLMHREVUpTenBTZlp3SG5EZ1dVQ3FJN2R1Vk5NUGYwbVN4eUdwRS8wbkxxcnJ1NWdUdWYwKzdoTmgwSDdicFBQeUtaSzlUZ0wxRjRkTkFGRW1PeThDTEt2UHIxa2IrbDZ1QzQvdFB0cXJNTlEvNHRIemJHcWRSR3QrRmRvT1BVcklUcXh5WTFPQ3pmQVVMaGlTMVVXUTBIUUZ0SmEzeFhLaTlCdjRubnlIbTA4SExwd0FUaS9Wdy9KSDVzaW1vUzF6SUVLT0ljRGttVnZBbENGWStlaFBqbS9QMkw2aGdLaDVuVW5Ka1pFdFltdGljOVlwdURMMDc0SHdRWEcxS0xzclNRWjB6cGs5RWYyY29QempORU9ZMFp6UWxsVXV4SXdXblNOSDk0VWRvY2hRRmxmeFpCR1JINjlpQlFNRmFqSDZYZDUySFpGUXhtRGFROWJtd0RWVWNvcHFSNXo2L3dJbz0iLCJkYXRha2V5IjoiQVFJQkFIaEFPc2FXMmdaTjA5V050TkdrWWM4cXAxMXhTaFovZHJFRW95MUhrOExYV2dFNHQxTzdUMVhoTnYvTDMxQXdkK09sQUFBQWZqQjhCZ2txaGtpRzl3MEJCd2FnYnpCdEFnRUFNR2dHQ1NxR1NJYjNEUUVIQVRBZUJnbGdoa2dCWlFNRUFTNHdFUVFNWk5NaU5rVVpvQjAyUmNDakFnRVFnRHZMcVcvQVB2UkpBaUFvK0Y0WFNjbms0RC9uSjQ3VytFSUlnZGcxRHBlOEJnVm1nTzFJb2cvRXl6L1N6VmxGRTJtL1poUGNkU0VmMDFUK1BRPT0iLCJ2ZXJzaW9uIjoiMiIsInR5cGUiOiJEQVRBX0tFWSIsImV4cGlyYXRpb24iOjE2NjY5MTU3OTZ9 ${ECR_REPO}"
                        sh "docker tag ${NAME}:latest ${ECR_REPO}"
                        sh "docker push ${ECR_REPO}"
                      // }
                    }catch(error){
                        print(error)
                        currentBuild.result = 'FAILURE'
                    }
                }
            }
            post{
                success {
                    echo "The ECR Upload stage successfully."
                }
                failure{
                    echo "The ECR Upload stage failed."
                }
            }
        }
    }
}