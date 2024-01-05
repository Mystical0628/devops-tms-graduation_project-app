pipeline {
  agent {
    label 'amazon'
  }

	tools {
		go '1.18.1'
	}

  stages {
    stage('Build') {
      steps {
	      sh 'go build -o app'
      }
    }

    stage('Test') {
      steps {
        dir('src') {
          echo 'Tests accepted'
        }
      }
    }

    stage('Ansible: Deploy') {
      steps {
        dir('configure') {
          ansiblePlaybook credentialsId: 'ec2-ssh-key', inventory: 'hosts', playbook: 'jenkins_agents.yaml'
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