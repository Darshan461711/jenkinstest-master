pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo 'Checkout'
            }
        }
        stage('Build') {
            steps {
                echo 'Clean Build'
                bat 'mvn clean compile'
            }
        }
        
        stage('Test') {
            steps {
                echo 'Testing'
                bat 'mvn test'
            }
        }
        stage('JaCoCo') {
            steps {
                echo 'Code Coverage'
                jacoco()
            }
        }
       stage("build & SonarQube analysis") {
            environment {
                scannerHome = tool 'SonarQubeScanner'
            }
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
	    
	    stage('Package')
	    {
	    	steps{
	    	  echo 'Package'
	    	  bat 'mvn package -DskipTests'    
	    	      
	    	  
	    	}
	    }
	    stage('Deploy')
	    {
	    	steps{
	    	  echo '## TO DO DEPLOYMENT ##'
	    	}
	    }
	   
	    stage('JUnit')
	     {
		     steps{
			       junit '/target/surefire-reports/*.xml'
		     }
	    }
	    stage('Qwikeye publisher'){
	    	steps{
	    	
	    	 qwikeye 'Darshan'
	    	}
	    
	    
	    }
	    
    }
    
    post {
        always {
            echo 'JENKINS PIPELINE'
        }
        success {
            echo 'JENKINS PIPELINE SUCCESSFUL'
        }
        failure {
            echo 'JENKINS PIPELINE FAILED'
        }
        unstable {
            echo 'JENKINS PIPELINE WAS MARKED AS UNSTABLE'
        }
        changed {
            echo 'JENKINS PIPELINE STATUS HAS CHANGED SINCE LAST EXECUTION'
        }
    }
}
