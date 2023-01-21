pipeline {
    agent any
    stages {
        stage('install puppet on slave') {
            steps {
                echo 'Install Puppet'
                sh "sudo apt-get install -y wget"
                sh "wget https://apt.puppetlabs.com/puppet-release-bionic.deb"
                sh "sudo dpkg -i puppet-release-bionic.deb"
                sh "sudo apt update"
                sh "sudo apt install -y puppet-agent"
            }
        }

        stage('configure and start puppet') {
            steps {
                echo 'configure puppet'
                sh "mkdir -p /etc/puppetlabs/puppet"
                sh "if [ -f /etc/puppetlabs/puppet/puppet.conf ]; then sudo rm -f /etc/puppetlabs/puppet.conf; fi"
                sh "echo '[main]\ncertname = node1.local\nserver = puppet' >> ~/puppet.conf"
                sh "sudo mv ~/puppet.conf /etc/puppetlabs/puppet/puppet.conf"
                echo 'start puppet'
                sh "sudo systemctl start puppet"
                sh "sudo systemctl enable puppet"
            }
        }

        stage('SCM Checkout') {
            steps {
                git 'https://github.com/banty105/edureka-project.git'
            }
        }
   
        stage('Execute Ansible') {
            steps {
                ansiblePlaybook credentialsId: 'forjenkisns', disableHostKeyChecking: true, installation: 'myansible', inventory: 'slave.inv', playbook: 'dockertest.yml'
            }
        }
    }
}
