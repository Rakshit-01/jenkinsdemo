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
          sh 'docker login -u AWS -p $(aws ecr-public get-login-password --region us-east-1) public.ecr.aws/o8b6i1z2' 
          sh 'docker build -t task .'
          sh 'docker tag task :latest public.ecr.aws/o8b6i1z2/task:""$BUILD_ID""'
          sh 'docker push public.ecr.aws/o8b6i1z2/task:""$BUILD_ID""'
         }
       }
    }
  }
}
