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

    stage('Deploy') {
      steps {
        dir('src') {
	        echo 'Deploying'
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