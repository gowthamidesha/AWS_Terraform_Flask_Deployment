pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-credentials')
        AWS_SECRET_ACCESS_KEY = credentials('aws-credentials')
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/gowthamidesha/AWS_Terraform_Flask_Deployment.git'
            }
        }

        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }

        stage('Terraform Plan') {
            steps {
                sh 'terraform plan -out=tfplan'
            }
        }

        stage('Terraform Apply') {
            steps {
                sh 'terraform apply -input=false -auto-approve tfplan'
            }
        }

        stage('Verification') {  // New stage for verification
            steps {
                echo 'Verifying deployment...'
                // Add verification steps here, e.g., using AWS CLI to check EC2 status
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}

