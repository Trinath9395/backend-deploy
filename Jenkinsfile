pipeline {
    agent { label 'AGENT-1' }
    environment {
        PROJECT     = 'expense'
        COMPONENT   = 'backend'
        DEPLOY_TO   = 'production'
        REGION      = 'us-east-1'
    }
    options {
        disableConcurrentBuilds()
        timeout(time: 30, unit: 'MINUTES')
    }
    parameters {
        string(name: 'PERSON',  description: 'Enter the application version')
        
    }
    stages {
        stage('Deploy') {
            steps {
                script{
                  withAWS(region: 'us-east-1', credentials: 'aws-creds') {
                    sh """
                       aws eks update-kubeconfig --region $REGION --name expense-dev
                       kubectl get nodes
                    """
                  }
                }
            }
        }
     
    }
    post {
        always {
            echo "I will always run this build"
            deleteDir()
        }
        failure {
            echo "I will run pipeline is failed"
        }
        success {
            echo "I will run pipeline is success"
        }
    }
}
