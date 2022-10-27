pipeline {
  agent {
      label 'qatest'
  }
  tools {
    maven 'Maven'
    jdk 'JDK8'
  }
  environment {
	VIRTUOSO_URL = 'qa.myapp.com'
  }
  stages {
    stage('intialize') {
      steps {
        sh '''
        echo "PATH= ${PATH}"
        echo "M3_HOME = ${M3_HOME}"
        '''
      }
    }
    stage('Execute Jmeter') {
      steps {
        sh 'pwd'
        	dir("scenarioLoadTests"){
        		sh 'pwd'
        		sh 'mvn clean verify'
       		 }
      	}
      	post{
      		always{
	      		dir("scenarioLoadTests/target/jmeter/results/"){
	        		sh 'C:\Users\SauravSharma\Downloads\apache-jmeter-5.5\apache-jmeter-5.5\bin\jmeter'
	    	 	}
      		
      		}
      	}
    }
  }
}
