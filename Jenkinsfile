pipeline { 
  
   agent any

   stages {
   
      stage('Install Dependencies') { 
        steps { 
           sh 'echo "Install dependencies" '
        }
     }
     
     stage('Test') {
       when {
         beforeAgent true
         anyOf {
           branch 'develop'; branch 'prod'
              }
       }
        steps { 
           sh 'echo "testing application..."'
        }
      }

         stage("Deploy application") { 
         steps { 
           sh 'echo "deploying application..."'
         }

     }
  
   	}

   }
