pipeline {
  agent any 
  environment {
    AWS_ACCOUNT_ID="360802824704" 
    AWS_DEFAULT_REGION="ap-south-1"
   IMAGE_REPO_NAME="jayk"
    IMAGE_TAG="latest"
    REPOSITORY_URI = "${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazon.com/${IMAGE_REPO_NAME}"
  }
    stages {
  stage('cloning Git') {
    steps {
      checkout scm
    }
  }

  stage('Building image') {
    steps{
      script {
        dockerImage = docker.build "${IMAGE_REPO_NAME}:${IMAGE_TAG}:${IMAGE_TAG}"
      }
    }
  }

  stage('pushing to ECR') {
    steps{
      script {
        sh "docker tag ${IMAGE_REPO_NAME}:$IMAGE_TAG"
        sh "docker push ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}:${IMAGE_TAG}"
        }
      }
    }
  }
}
