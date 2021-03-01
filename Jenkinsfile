pipeline {
    agent any 

        parameters {
        string(name: 'environment', defaultValue: 'default', description: 'Workspace/environment file to use for deployment')
        string(name: 'version', defaultValue: '', description: 'Version variable to pass to Terraform')
        booleanParam(name: 'autoApprove', defaultValue: false, description: 'Automatically run apply after generating plan?')
    }
    
    environment {
        AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
        TF_IN_AUTOMATION      = '1'
    }

    stages {
        stage('Test') {
            steps {
                sh 'aws iam get-user'
            }
        }

        stage('TF Plan') {
            steps {
                script {
                    currentBuild.displayName = params.version
                }
                sh 'terraform init -input=false'
                sh 'terraform workspace select ${environment}'
                sh "terraform plan -input=false -out tfplan -var 'version=${params.version}' --var-file=environments/${params.environment}.tfvars"
                sh 'terraform show -no-color tfplan > tfplan.txt'
            }
        }
    }
}