pipeline {
  agent any

  environment {
    AWS_REGION   = "us-east-1"
    AWS_ACCOUNT  = "698748551201"
    ECR_REPO     = "learn/spring-helloworld"
    ECR_REGISTRY = "${AWS_ACCOUNT}.dkr.ecr.${AWS_REGION}.amazonaws.com"
    IMAGE_NAME   = "${ECR_REGISTRY}/${ECR_REPO}"
  }

  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Build & Push Image (Jib)') {
      steps {
        withCredentials([usernamePassword(
          credentialsId: '239362d5-8f39-407c-b9a6-f21c89b89af9',        
          usernameVariable: 'AWS_ACCESS_KEY_ID',
          passwordVariable: 'AWS_SECRET_ACCESS_KEY'
        )])
        {
        sh '''

          echo "Key prefix used by Jenkins: ${AWS_ACCESS_KEY_ID:0:6}"

        '''
        }
      }
    }
  }
}
