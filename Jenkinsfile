
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
        }
        failure {
            echo '❌ Deployment failed!'
        }
    }
}