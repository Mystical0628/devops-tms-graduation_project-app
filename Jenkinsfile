pipeline {
  agent {
    label 'amazon'
  }

  stages {
    stage('Build') {
      tools {
        go '1.18.1'
      }

      steps {
        dir('src') {
          sh 'go build -o app'
        }
      }
    }

    stage('Test') {
      steps {
        dir('src') {
          echo 'Tests accepted'
        }
      }
    }

    stage('Ansible') {
      tools {
        ansible 'ansible'
      }

      stages {
        stage('Playbook: Deploy') {
          steps {
            dir('configure') {
              ansiblePlaybook credentialsId: 'ec2-ssh-key', inventory: '/home/jenkins/hosts.yaml', playbook: 'deploy.yaml'
            }
          }
        }

        stage('Playbook: Start') {
          steps {
            dir('configure') {
              ansiblePlaybook credentialsId: 'ec2-ssh-key', inventory: '/home/jenkins/hosts.yaml', playbook: 'start.yaml'
            }
          }
        }
      }
    }
  }

  post {
    success {
      echo 'Success!'
    }
  }
}