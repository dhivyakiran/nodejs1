pipeline  {   
agent
{
   label "slave1"
}
environment
   {
      lastfile=0
   }
stages  
{ 
   stage('Trigger the microservice pipeline job')  
   {
      steps  
      {
         script 
         {
            def filename
            def changeLogSets = currentBuild.changeSets
            for (int i = 0; i < changeLogSets.size(); i++) 
            {
              def entries = changeLogSets[i].items
              for (int j = 0; j < entries.length; j++) 
              {
                 def entry = entries[j]
                 def files = new ArrayList(entry.affectedFiles)
                 for (int k = 0; k < files.size(); k++) 
                 {
                    def file = files[k]
                    echo "${file.path}"
                    filename=file.path
                    if((filename == "dev.yml" || filename == "int.yml" || filename == "qa.yml"))
                    {
                        lastfile=1
                    }
                  }
               }
             }
             if(lastfile==1)
             {
                def filevalue=filename.split(/\./)
                echo "${filevalue}"
                echo "Triggered the portal pipeline"
                build job: 'microservice-pipeline',  parameters: [[$class: 'StringParameterValue', name: 'envname', value: "${filevalue[0]}"]], wait: true
             }
           }
        }
     }
  }
}
