pipeline {
    agent any
    parameters {
        booleanParam(name:'AutoApprove', defaultValue: false, description: 'Auto approve the deployment')
        choice(name:'action', choices:['apply','destroy'], description:'select action')
    }

    environment {
        AWS_REGION = 'us-east-1'
    }

    stages {
        stage('init'){
            steps {
                sh 'terraform init'
            }
        }
        stage('test'){
            steps {
                sh 'terraform plan -out=tfplan'
                sh 'terraform show -no-color tfplan > tfplan.txt'

            }
        }
        stage('build'){
            steps {
                echo 'Building...'
            }
        }
        stage('deploy'){
            steps {
                echo 'Deploying...'
            }
        }
    }
}