pipeline{
    agent any

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
                git url:"${GIT_URL}", branch:"main", poll:true, changelog:true,credentialsId: "${GIT_CREDENTIAL_ID}"
            }
        }
        stage('Build') {
            steps {
                sh "docker build -t ${NAME} ."
                // sh "docker tag ${NAME}:latest ${NAME}:latest"
            }
        }
        // stage('ECR Upload'){
        //     steps {
        //         script{
        //             try{
        //                 withAWS(credentials: "${AWS_CREDENTIALS}", role: 'arn:aws:iam::347222812711:user/deploy_user:role/jenkins-deploy-role', roleAccount: "deploy_user", externalId: 'externalId'){
        //                     sh "aws ecr get-login-password --region ap-northeast-2 | docker login --username AWS --password-stdin 347222812711.dkr.ecr.ap-northeast-2.amazonaws.com/test_cicd"
        //                     sh "docker push ${ECR_REPO}/${NAME}:latest"
        //                 }
        //             }catch(error){
        //                 print(error)
        //                 currentBuild.result = 'FAILURE'
        //             }
        //         }
        //     }
        //     post{
        //         success {
        //             echo "The ECR Upload stage successfully."
        //         }
        //         failure{
        //             echo "The ECR Upload stage failed."
        //         }
        //     }
        // }
    }
}