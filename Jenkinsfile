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
          sh 'docker login -u AWS -p $(aws ecr public  get-login-password --region ap-south-1) 517738790203.dkr.ecr.ap-south-1.amazonaws.com' 
          sh 'docker build -t ecr-demonimg .'
          sh 'docker tag ecr-demonimg :latest 517738790203.dkr.ecr.ap-south-1.amazonaws.com/task:""$BUILD_ID""'
          sh 'docker push 517738790203.dkr.ecr.ap-south-1.amazonaws.com/task:""$BUILD_ID""'
         }
       }
    }
  }
}
