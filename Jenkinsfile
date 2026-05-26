pipeline {
    agent {
        node {
            label 'AGENT-1'
        }
    } 
    options {
        disableConcurrentBuilds()
        ansiColor('xterm')
        timeout(time: 1, unit: 'HOURS')
    }

    parameters {
        string(name: 'VERSION', defaultValue: '', description: 'What is the Version?')

        string(name: 'ENVIRONMENT', defaultValue: '', description: 'What is the Environment?')
    }
    stages {
        stage('Get the Package Version & Environment from CATALOGUE-CI') {
            steps {
                echo "Version: ${params.VERSION}"

                echo "environment: ${params.ENVIRONMENT}"
            }
        }
        stage('Terraform Initializing') {
            steps {
                sh """
                    cd terraform
                    terraform init --backend-config=${params.ENVIRONMENT}/backend.tf -reconfigure
                """
            }
        }
        stage('Terraform Planning') {
            steps {
                sh """
                    cd terraform
                    terraform plan -var-file=${params.ENVIRONMENT}/${params.ENVIRONMENT}.tfvars -var="app_version=${params.VERSION}"
                """
            }
        }
    }
    post {
        always {
            echo 'PIPELINE EXECUTION IS COMPLETED'
        }
        failure {
            echo 'The pipeline is FAILED'
        }
        success {
            echo 'The pipeline is SUCESS'
        }
    }
}