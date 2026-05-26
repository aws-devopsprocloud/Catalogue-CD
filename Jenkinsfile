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
        stage('Print the Package Version & Environment from CATALOGUE-CI') {
            steps {
                echo "Version: ${params.VERSION}"

                echo "environment: ${params.ENVIRONMENT}"
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