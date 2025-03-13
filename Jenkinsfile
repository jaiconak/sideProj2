pipeline {
    agent any

    environment {
        AWS_REGION = "us-east1"
        IMAGE_ECR_REPO = "039612867339.dkr.ecr.us-east-1.amazonaws.com/jenkins-registry-jaico"
        ECR_REPO = "039612867339.dkr.ecr.us-east-1.amazonaws.com"

    }
    stages {
        stage ("Code Scan") {
            steps {
                sh "trivy fs . -o result.html"
                sh "cat result.html"
            }
        }
        stage ("dockerLogin"){
            steps {
                sh "aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin $ECR_REPO"

            }
        }
        stage ("dockerImageBuild") {
            steps {
                sh "docker build -t jenkins-registry-jaico ."
                sh "docker build -t imageversion ."
            }
        }
        stage ("dockerTag") {
            steps {
                sh "docker tag jenkins-registry-jaico:latest $IMAGE_ECR_REPO:latest"
                sh "docker tag jenkins-registry-jaico:latest $IMAGE_ECR_REPO:v1.${BUILD_NUMBER}"
            }
        }
        stage ("pushImage") {
            steps {
                sh "docker push $IMAGE_ECR_REPO:latest"
                sh "docker push $IMAGE_ECR_REPO:v1.${BUILD_NUMBER}"
            }
        }
    }
}