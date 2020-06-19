pipeline {
    agent none  
    parameters {
        string(name: 'gitBranch', defaultValue: 'master', description: 'Specify your source code branch.')
    }    
    stages {

        stage('Cleanup') {
            agent {
                node {
                    label 'master'
                }
            }
            steps {
                script{
                    sh """
                        rm -rf /tmp/jenkins-ansible
                    """
                }
            }
        }

        stage('Deploy') {
            agent {
                node {
                    label 'master'
                    customWorkspace '/tmp/jenkins-ansible'
                }
            }
            steps {
                script{
                    sh """
                        git clone --single-branch --branch ${params.gitBranch} https://github.com/akai0211/jenkins-ansible-helloworld.git .
                        ansible-playbook sample-playbook.yml
                    """
                }
            }
        }        
    }
}