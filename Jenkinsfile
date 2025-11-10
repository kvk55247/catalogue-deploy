pipeline {
   agent {
        node {
            label 'AGENT-1'
        }
    }
    environment {
        appVersion = ''
        REGION = "us-east-1"
        ACC_ID = "784585544641"
        PROJECT = "roboshop"
        COMPONENT = "catalogue"

    }
    options {
        timeout(time: 30, unit: 'MINUTES') 
        disableConcurrentBuilds()
    } 
    parameters {
        string(name: 'appVersion',  description: 'image version of the application') 
        choice(name: 'deploy_to', choices: ['dev', 'qa', 'prod'], description: 'Pick the environment')
    } 
// build
    stages {
        stage('deploy') {
            steps {
                script {
                    withAWS(credentials: 'aws-creds', region: 'us-east-1') {
                         sh """  
                             aws eks update-kubeconfig --region $REGION --name "$PROJECT-${params.deploy_to}" 
                             kubectl get nodes
                         """
                }
            }
        }
    }
}
    post { 
        always { 
            echo 'I will always say Hello again!'
        }
        success {
            echo 'hi this is success'
            deleteDir()
        }
        failure {
            echo 'hi, this is failure'
        }
    }
}
    
