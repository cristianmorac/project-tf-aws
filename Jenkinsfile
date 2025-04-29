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
        stage('checkout'){
            steps {
                /* Toma el repositorio configurado y la rama */
                checkout scm
            }
        }
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
        stage('build Apply or destroy'){
            steps {
                script {
                    if (params.action == 'apply'){
                        if (!params.AutoApprove){
                            def plan = readFile 'tfplan.txt'
                            input message: 'Do you want to apply the plan?'
                            parameters: [text(name: 'Plan', description: 'Please review the plan', defaultValue: plan)]
                        }
                         sh 'terraform ${action} -input=false tfplan'
                    } else if (params.action == 'destroy'){
                        sh 'terraform ${action} --auto-approve'
                    } else {
                        error "Invalid action selected. Please choose either 'apply' or 'destroy'."
                    }
                }
            }
        }
        stage('deploy'){
            steps {
                echo 'Deploying...'
            }
        }
    }
}