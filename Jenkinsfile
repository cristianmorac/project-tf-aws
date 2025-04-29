pipeline {
    agent any
    paramaters {
        booleanParam(name:'AutoApprove', defaultValue: true, description: 'Auto approve the deployment')
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
                echo 'Running tests...'
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