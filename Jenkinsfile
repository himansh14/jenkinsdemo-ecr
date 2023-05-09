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
        withEnv (["AWS_ACCESS_KEY_ID=${env.AWS_ACCESS_KEY_ID}", "AWS_SECRET_ACCESS_KEY=${env.AWS_SECRET_ACCESS_KEY}", "AWS_DEFAULT_REGION=${env.AWS_DEFAULT_REGION}"]) {
          sh 'docker login -u AWS -p $(aws ecr-public get-login-password --region us-east-1) public.ecr.aws/c9n1s5l2'
          sh 'docker build -t ecr-repo .'
          sh 'docker tag ecr-repo:latest public.ecr.aws/c9n1s5l2/ecr-repo:latest1 {print $2 += .01; exit}'
          sh 'docker push public.ecr.aws/c9n1s5l2/ecr-repo:latest1 {print $2 += .01; exit}'
         }
       }
    }
  }
}
