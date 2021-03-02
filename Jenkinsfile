pipeline {
    agent any 

    stages {
        stage('Test') {
            steps {
                sh 'aws iam get-user'
            }
        }

        stage('TF Plan') {
            steps {
                sh 'terraform --version'
            }
        }
    }
}