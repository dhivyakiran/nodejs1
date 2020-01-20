pipeline  {   
agent
{
   label "master"
}
environment
   {
      microservice1=0
      microservice2=0
   }
stages  
{
   stage('Checking out first') {
      steps {
          dir('microservice1') {
            git(url: 'https://github.com/dhivyakiran/nodejs1.git', branch: 'master')
         }
      }
    }
    stage('Checking out second') {
      steps {
          dir('microservice2') {
            git(url: 'https://github.com/dhivyakiran/helloworld-nodejs.git', branch: 'master')
         }
      }
    }
   stage('Clone sources')  
   {
      steps  
      {
         script 
         {
            String repoUrl1 = 'https://github.com/dhivyakiran/helloworld-nodejs.git'
             String repoUrl2 = 'https://github.com/dhivyakiran/nodejs1'
            def filename
            def changeLogSets = currentBuild.changeSets
           for (int i = 0; i < changeLogSets.size(); i++) {
           def entries = changeLogSets[i].items
           for (int j = 0; j < entries.length; j++) {
               def entry = entries[j]
              def lastId = entry.commitId
              echo "last id : ${lastId}"
            echo "${commitInfo(entry)}"
              def geturl="${repoUrl2}/git/commits/${lastId}",
                 echo "url: ${geturl}"
               def files = new ArrayList(entry.affectedFiles)
               for (int k = 0; k < files.size(); k++) {
                   def file = files[k]
                   echo "${file.path}"
                  filename=file.path
                  
                    if((repoUrl1 && (filename == "dev.yml" || filename == "int.yml" || filename == "qa.yml")))
                       {
                          echo "file get into microservice1"
                          microservice1=1
                          break
                       }
                   if((repoUrl2 && (filename == "dev.yml" || filename == "int.yml" || filename == "qa.yml")))
                       {
                          echo "file get into microservice2"
                          microservice2=1
                          break
                       }
                  
               }
           }
           }
            
           /* if(lastfile==1)
            {
                def filevalue=filename.split(/\./)
            echo "${filevalue}"
               echo "get into pipeline"
               build job: 'microservice-pipeline',  parameters: [[$class: 'StringParameterValue', name: 'envname', value: "${filevalue[0]}"]], wait: true
            }*/
         }
      }
   }
}
}
