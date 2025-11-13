
pipeline {
    agent any
    
    environment {
        INVENTORY = 'ansible/inventory.ini'
        PLAYBOOK = 'ansible/setup_apps.yml'
    }
    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/Abhi1121-linux/devops-project.git', branch: 'main'
            }
        }
        stage('Run Ansible Playbook') {
            steps {
                ansiblePlaybook(
                    playbook: "${PLAYBOOK}",
                    inventory: "${INVENTORY}",
                    colorized: true
                )
            }
        }
    }
    post {
        success {
            echo '✅ All apps installed and started successfully!'
            emailext (
                to: 'test112107@gmail.com',
                subject: "✅ Jenkins Build SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Good news!\n\nThe Jenkins build '${env.JOB_NAME} #${env.BUILD_NUMBER}' was successful.\nCheck console output: ${env.BUILD_URL}",
                
            )
        }
        failure {
            echo '❌ Deployment failed!'
            emailext (
                to: 'test112107@gmail.com',
                subject: "❌ Jenkins Build FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Attention!\n\nThe Jenkins build '${env.JOB_NAME} #${env.BUILD_NUMBER}' has failed.\nCheck console output: ${env.BUILD_URL}",   
                               
            )
        } 
    }
}   