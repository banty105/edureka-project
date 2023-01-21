pipeline {
    agent slaveNode

    stages {
        stage('SCM Checkout') {
            steps {
                git 'https://github.com/banty105/edureka-project.git'
            }
        }
    }

    stages {
        stage('Execute Ansible') {
            steps {
                ansiblePlaybook credentialsId: 'forjenkisns', disableHostKeyChecking: true, installation: 'myansible', inventory: 'slave.inv', playbook: 'dockertest.yml'
            }
        }
    }
}
