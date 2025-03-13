pipeline {
    agent any
    stages {
        stage ('Code Scan') {
            steps {
                sh 'trivy fs . -o result.html'
                sh 'cat result.html'
            }
        }
        stage ('dockerLogin'){
            steps {
                sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 039612867339.dkr.ecr.us-east-1.amazonaws.com'

            }
        }
        stage ('dockerImageBuild') {
            steps {
                sh 'docker build -t jenkins-registry-jaico .'
            }
        }
        stage ('dockerTag') {
            steps {
                sh 'docker tag jenkins-registry-jaico:latest 039612867339.dkr.ecr.us-east-1.amazonaws.com/jenkins-registry-jaico:latest'
            }
        }
        stage ('pushImage') {
            steps {
                sh 'docker push 039612867339.dkr.ecr.us-east-1.amazonaws.com/jenkins-registry-jaico:latest'
            }
        }
    }
}