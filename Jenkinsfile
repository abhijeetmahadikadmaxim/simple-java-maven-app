pipeline {
  agent {
    docker {
      image 'maven:3-alpine'
      args '-v /root/.m2:/root/.m2'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
      }
    }

    stage('Test and deploy') {
      post {
        always {
          junit 'target/surefire-reports/*.xml'
        }

      }
      steps {
        sh 'mvn test'
        input ' Finished using the web site? (Click "Proceed" to continue)'
        sh './jenkins/scripts/deliver.sh'
      }
    }

  }
  environment {
    CI = 'true'
  }
}