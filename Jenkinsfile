pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }
        stage('Terraform Init') {
            steps {
                script {
                    sh 'terraform init'
                }
            }
        }
        stage('Terraform Plan') {
            steps {
                script {
                    sh 'terraform plan -var "do_token=${DO_PAT}"  -var "pvt_key=$HOME/.ssh/id_rsa" -out=tfplan'
                }
            }
        }
        stage('Terraform Apply') {
            steps {
                script {
                    sh 'terraform apply -var "do_token=${DO_PAT}"  -var "pvt_key=$HOME/.ssh/id_rsa" -auto-approve tfplan'
                }
            }
        }
      }
    post {
        always {
            cleanWs()
        }
    }
}
