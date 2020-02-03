pipeline  
{   
	agent
	{
		label "master"
	}
	environment
	{
		lastfile=0
	}
	stages  
	{ 
		stage('Triggering pipeline')  
		{
			steps  
			{
				script 
				{
					
				    lastfile = sh(returnStdout: true, script: 'git diff-tree --no-commit-id --name-status -r HEAD').trim()
					if (lastfile.indexOf('qa.yml')< 0 && lastfile.indexOf('int.yml')< 0 && lastfile.indexOf('uat.yml')< 0 && lastfile.indexOf('prod.yml')< 0)
					{
						    echo "Triggered................."
							build job: 'microservice-pipeline',  parameters: [[$class: 'StringParameterValue', name: 'envname', value: "dev"]], wait: true
							
							
							
					}
					
				}
			}
		}
	}
}
     
	 
	 
	 
	 


























