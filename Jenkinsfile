pipeline {
  agent any
  stages {
    stage ('Build') {
      steps {
        sh 'printenv'
      }
    }
    stage ('Publish to ECR') {
      steps {
         withEnv(["AWS_ACCESS_KEY_ID=${env.AWS_ACCESS_KEY_ID}", "AWS_SECRET_ACCESS_KEY=${env.AWS_SECRET_ACCESS_KEY}", "AWS_DEFAULT_REGION=${env.AWS_DEFAULT_REGION}"]) {
          sh 'docker login -u AWS -p $(aws ecr get-login-password --region ap-south-1) public.ecr.aws/o8b6i1z2' 
          sh 'docker build -t ecr-demonimg .'
          sh 'docker tag ecr-demonimg :latest public.ecr.aws/o8b6i1z2:""$BUILD_ID""'
          sh 'docker push public.ecr.aws/o8b6i1z2:""$BUILD_ID""'
         }
       }
    }
  }
}
