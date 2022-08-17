def genaralvars () {

    env.GIT_REPO = 'https://github.com/TheIronhidex/ansible01/tree/main'
    env.GIT_BRANCH = 'main'
    env.DOCKER_REPO = 'theironhidex'
    CONTAINER_PORT= '87'

}

pipeline {
    agent any
    //tool name: 'ansible210', type: 'org.jenkinsci.plugins.ansible.AnsibleInstallation'
    stages {
        stage ("Set Variables") {
            steps {                
                genaralvars()
            }
        }
        stage ("Get Code") {
            steps {
                git branch: "${env.GIT_BRANCH}", url: "${env.GIT_REPO}"
            }
        }
        stage ("Ansible Hello World") {
            steps {
                ansiblePlaybook become: true, colorized: true, extras: '-v', disableHostKeyChecking: true, credentialsId: 'gonzafirma-ssh-server01', installation: 'ansible210', inventory: 'inventory.hosts', playbook: 'playbook-hello-world.yml'
            }
        }
        stage ("Ansible Connect to HOST and Install Package") {
            steps {
                ansiblePlaybook become: true, colorized: true, extras: '-v', disableHostKeyChecking: true, credentialsId: 'gonzafirma-ssh-server01', installation: 'ansible210', inventory: 'inventory.hosts', playbook: 'playbook-install-package-ubuntu.yml'
            }
        }
        stage ("Ansible Connect to HOST and execute a command") {
            steps {
                ansiblePlaybook become: true, colorized: true, extras: '-v', disableHostKeyChecking: true, credentialsId: 'gonzafirma-ssh-server01', installation: 'ansible210', inventory: 'inventory.hosts', playbook: 'playbook-execute-command.yml'
            }
        }
        stage('Manual Approval to Uninstall Package') {
            steps{
                input "Proceed to Uninstall Package?"
            }
        }
        stage ("Ansible Connect to HOST and Uninstall Package") {
            steps {
                ansiblePlaybook become: true, colorized: true, extras: '-v', disableHostKeyChecking: true, credentialsId: 'gonzafirma-ssh-server01', installation: 'ansible210', inventory: 'inventory.hosts', playbook: 'playbook-uninstall-ubuntu-package.yml'
            }
        }
    }
}
