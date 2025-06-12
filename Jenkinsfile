pipeline {
    agent any

    environment {
        ANSIBLE_FORCE_COLOR = "true"
        ANSIBLE_HOST_KEY_CHECKING = "False"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/snc20/first1.git'
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sh 'ansible-playbook -i inventory/hosts.yml playbooks/site.yml -c local --become'
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
