
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
          }
}
