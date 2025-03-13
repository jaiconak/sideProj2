pipeline {
    agent any
    stages {
        stage ('checkout') {
            steps {
                sh 'echo "Jaico YOU GOT THIS!"'
            }
        }
        stage ('test') {
            steps {
                sh 'echo "testing!!"'
            }
        }
        stage ('create File') {
            steps {
                sh 'touch text-${BUILD_ID}'
            }
        }
    }
}