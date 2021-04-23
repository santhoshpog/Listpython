pipeline {
    agent {
        node {
            label 'PROD'
        }
    }
        stages {
            stage('Cloning Repo') {
                steps {
                    git branch: 'main', url: 'https://github.com/santhoshpog/Listpython.git'
                }
            }
        stage('Running Other Programs') {
            parallel {
                stage('Running Evenodd.py') {
                    steps {
                        sh 'python evenodd.py'
                    }
                }
                stage('Running mydict.py') {
                    steps {
                        sh 'python mydict.py'
                    }
                }
                stage('Running Ansible') {
                    steps {
                        sh 'yum install -y epel-release && yum install -y ansible'
                    }
            }
                stage('Executing Ansible Yaml for Docker installation') {
                    steps {
                        sh 'ansible-playbook new.yml'
                    }
            }
		}
		}
        stage('Running Deployment') {
            steps {
                sh 'python deploy.py'
            }
        }
    }
}
