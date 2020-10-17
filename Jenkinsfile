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
	def USER_INPUT = input(
		message: 'User input required - Some Yes or No question?',
		parameters: [
			[class: 'ChoiceParameterDefinition',
			 choices: ['RTB1FR','RTB1SP','RTB3','RTB5','Abort'].join('\n'),
			 name: 'input',
			 description: 'Menu - select box option']
		])
	echo "The answer is: ${USER_INPUT}"
	
     		switch("${USER_INPUT}"){
			case 'RTB1FR':
				sh './jenkins/scripts/deliver.sh'
				break;
        	        case 'RTB1SP':
                       		sh './jenkins/scripts/deliver.sh'
                	        break;

                	case 'RTB3':
                        	sh './jenkins/scripts/deliver.sh'
                        	break;

                	case 'RTB5':
                        	sh './jenkins/scripts/deliver.sh'
                        	break;

                	case 'Abort':
                        	break;
			default :
				break;
	}	
      }
    }

  }
  environment {
    CI = 'true'
  }
}
