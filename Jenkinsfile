pipeline { 
  environment {
    week = "Sunday"
  }
   agent any
   stages {
   
      stage('Install Dependencies') { 
        steps { 
           sh 'echo "Install dependencies" '
        }
     }
     
     stage('Day'){
       steps{
         string v = sh(returnStdout: true, script: 'date +%a')
         print v
         print v.trim()
       }
     }
     
     stage('Test') {
       when {
         beforeAgent true
        // anyOf {
         //       branch 'prod'; branch 'release'
         //       }
         allOf {
                //branch 'develop'
                expression{env.BRANCH_NAME == 'develop'}
                //expression{ week[new Date()[Calendar.DAY_OF_WEEK]] == 'Sunday' }
                expression{ sh(returnStdout: true, script: 'date +%a') == 'Mon' }
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
