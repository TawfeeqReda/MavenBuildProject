node('master') {
  ansiColor('xterm') {
	stage ('checkout code'){
		checkout scm
	}
	node('slave01') {
	stage ('Build'){
		sh "mvn clean install -Dmaven.test.skip=true"
	}
	  
	

	stage ('Test Cases Execution'){
		sh "mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install -Pcoverage-per-test"
	}
	}
	  node('slave2') {

	stage ('Archive Artifacts'){
		archiveArtifacts artifacts: 'target/*.war'
	}
	  }
	
	stage ('Deployment'){
 
	}
	stage ('Notification'){
		//slackSend color: 'good', message: 'Deployment Sucessful'
		emailext (
		      subject: "Job Completed",
		      body: "Jenkins Pipeline Job for Maven Build got completed !!!",
		      to: "tawfeeq_it@hotmail.com"
		    )
	}
   }
}
