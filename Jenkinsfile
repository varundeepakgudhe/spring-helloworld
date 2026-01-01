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

    stage('Login to ECR') {
      steps {
        sh '''
          aws ecr get-login-password --region ${AWS_REGION} \
            | docker login --username AWS --password-stdin ${ECR_REGISTRY}
        '''
      }
    }

    stage('Build & Push Image (Jib)') {
      steps {
        sh '''
          chmod +x mvnw || true
          ./mvnw -DskipTests \
            -Dgit.commit=${GIT_COMMIT} \
            compile jib:build
        '''
      }
    }
  }
}
