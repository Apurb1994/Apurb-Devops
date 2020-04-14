
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
		                        	nexusArtifactUploader artifacts: [[artifactId: 'Apurb-Devops', classifier: 'debug', file: 'target/Apurb-Devops.war', type: 'war']],
									 credentialsId: 'nexus3', 
									 groupId: 'in.javahome', 
									 nexusUrl: '172.31.43.5:8081',
									  nexusVersion: 'nexus3',
									   protocol: 'http',
									    repository: 'Apurb-Devops-snapshot', 
										version: '2.0-SNAPSHOT'
		                       	}
		               	}
          }
}
