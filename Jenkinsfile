pipeline {
    agent any

    environment {
        ANSIBLE_FORCE_COLOR = "true"
        ANSIBLE_HOST_KEY_CHECKING = "False"
        ANSIBLE_BECOME_PASSWORD = '1'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/snc20/final.git'
            }
        }

        stage('Run Ansible Playbook') {
            steps {
               sh '''
ansible-playbook -i inventory/hosts.yml playbooks/site.yml \
-c local --become -e ansible_become_password=$ANSIBLE_BECOME_PASSWORD \
-M ./roles
'''

            }
        }
    }

    post {
        failure {
            echo 'Deployment failed.'
        }
        success {
            echo 'Ansible executed successfully.'
        }
    }
}
