pipeline {
    agent any 
    stages {
        stage('SetUp') { 
            steps {
                git 'https://github.com/mkam/ansible-example'
            }
        }
        stage('Deploy') { 
            steps {
                withCredentials([usernamePassword(credentialsId: 'SSH_CREDENTIALS', 
                        passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]){
                    ansiColor('xterm') {
                        ansiblePlaybook(colorized: true, 
                            extras: '-e ansible_ssh_user=$USERNAME -e "ansible_ssh_pass=$PASSWORD"', 
                            inventory: 'jenkins-hosts', 
                            playbook: 'install_python.yml', 
                            disableHostKeyChecking: true)
                    }
                }
            }
        }
        stage('Test') { 
            steps {
                print "Tests run here!" 
            }
        }
    }
}

