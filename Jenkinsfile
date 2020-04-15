
pipeline{
	agent any
	tools {
  maven 'maven7'
            }

	stages{
			    stage('Git Checkout')
		    	{
			    	steps{
		                    	git credentialsId: 'github', url: 'https://github.com/Apurb1994/Apurb-Devops'
		                	}
		    	}
			 
	
		            	stage('mvn build/package')
		            	{
		            		steps{
		                        	sh 'mvn clean package'
		                       	}
		               	}
						   stage('Nexus deploy')
		            	{
							
		            		steps{
								script
								{
									def pomfile = readMavenPom file: 'pom.xml'
									def version = pomfile.version
									def nexusRepo= version.endsWith("SNAPSHOT") ? "Apurb-Devops-snapshot": "Apurb-Devops"
		                        	nexusArtifactUploader artifacts: [[artifactId: 'Apurb-Devops', classifier: 'debug', file: 'target/Apurb-Devops.war', type: 'war']],
									 credentialsId: 'nexus3', 
									 groupId: 'in.javahome', 
									 nexusUrl: '172.31.43.5:8081',
									  nexusVersion: 'nexus3',
									   protocol: 'http',
									    repository: nexusRepo, 
										version: version
								}	
		                       	} 

		               	}
						   stage('Deploy Tomcat')
		            	{
		            		steps{
									sshagent(['tomcat-dev-ppk']) {
										sh "scp -o StrictHostKeyChecking=no target/*.war ec2-user@172.31.33.102: /opt/tomcat8/webapp/Apurb-Devops.war"
										sh "ec2-user@172.31.33.102: /opt/tomcat8/bin/shutdown.sh"
										sh "ec2-user@172.31.33.102: /opt/tomcat8/bin/startup.sh"
												}





		                        		                       	}
		               	}
          }
	post {
  success {
    mail bcc: '', body: '''Hi Devops Team,

 Build has been successfully generated''', cc: '', from: '', replyTo: '', subject: 'Build - Success', to: 'catchapurb1994gmail.com'.
  }
  failure {
    mail bcc: '', body: '''Hi Devops Team,

 Build has been successfully generated''', cc: '', from: '', replyTo: '', subject: 'Build - Failed', to: 'catchapurb1994gmail.com'
  }
}

}
