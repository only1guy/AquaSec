pipeline {
    agent any 

    tools {
        terraform 'Terraform'
    }
    
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