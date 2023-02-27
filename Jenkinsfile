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
          sh ' sudo docker login -u AWS -p $(aws ecr get-login-password --region ap-south-1) 517738790203.dkr.ecr.ap-south-1.amazonaws.com' 
          sh ' sudo docker build -t jenkins .'
          sh ' sudo docker tag jenkins:latest 517738790203.dkr.ecr.ap-south-1.amazonaws.com/jenkins:latest:'
          sh ' sudo docker push jenkins:latest 517738790203.dkr.ecr.ap-south-1.amazonaws.com/jenkins:latest'
         }
       }
    }
