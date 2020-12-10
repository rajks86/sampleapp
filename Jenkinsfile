pipeline {
  agent any
  tools {
    maven 'Maven'
  }
  stages {
    stage ('Initialize') {
      steps {
        sh '''
		echo "PATH = $(PATH)"
	   '''

      }
    }

    stage ('Build') {
      steps {
        sh 'mvn clean package'
      }
    }
    
    stage ('Deploy-to-Tomcat') {
      steps {
        sshagent (['appserver-key']) {
          sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@13.235.27.154:/var/lib/tomcat9/webapps/webapp.war'
        }
      }
    }
  }
}
