pipeline {
	environment {
        props = readYaml file: 'project.yaml'
    }
    stages {
	    stage('SCM Checkout') {
			steps {	
			  logInfo(" SCM Checkout Started !!!")		
			  cleanWs notFailBuild: true
			  checkout scm
   	  		  logInfo(" Complete - SCM Checkout !!!")

			}
		}
		stage('Build'){
			 steps {
				sh '''
				    echo -e " Executing in host : "`hostname`
					groupId=com.devops.azure
					mvn -f pom.xml clean package test verify sonar:sonar cobertura:cobertura deploy -Dgroup_id="$groupId" -Dartifact_id="$artifactId" -Dartifact_version="1.0.0.3"
				'''
			 }
		}

    }
	post {
		always {
			logInfo("POST DEPLOYMENT ACTIVITIES STARTED!!!")
		}
		failure {
        }
		success {
		
        }
	}
}

def logInfo(def infoMessage){
      println ("\n------------------------------------------------------------------------------------------")
      println (" [INFO] $infoMessage")
      println ("--------------------------------------------------------------------------------------------\n")	
}

def logError(def errorMessage){

      println ("\n------------------------------------------------------------------------------------------")
      println ("[ERROR] $errorMessage")
      println ("[ERROR] DEPLOYMENT FAILED !!!")
      println ("--------------------------------------------------------------------------------------------\n")	
	
}

def logWarning(def warningMessage){
      println ("\n------------------------------------------------------------------------------------------")
      println (" [INFO] $warningMessage")
      println ("--------------------------------------------------------------------------------------------\n")	
}
