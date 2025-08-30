pipeline {
    agent any

    environment {
        ANSIBLE_PLAYBOOK = "/home/ansible/java-restart/restart_buggyapp.yml"
        ANSIBLE_INVENTORY = "/home/ansible/java-restart/inventory.ini"
    }

    stages {
        stage('Checkout Code') {
            steps {
                script {
                    git branch: 'main',
                        credentialsId: 'github-token',  // Use the ID you set in Jenkins
                        url: 'https://github.com/Sumanth17-git/restart-java-ansible.git'
                }
            }
        }
        stage('Run Ansible Playbook') {
            steps {
                script {
                    echo "Executing Ansible playbook as ansible user"

                    def ansibleCommand = "sudo -u ansible ansible-playbook -i ${ANSIBLE_INVENTORY} ${ANSIBLE_PLAYBOOK}"
                    
                    sh ansibleCommand
                }
            }
        }
    }

    post {
        success {
            echo "Ansible playbook executed successfully!"
        }
        failure {
            echo "Ansible playbook execution failed!"
            error "Stopping pipeline due to failure"
        }
    }
}
