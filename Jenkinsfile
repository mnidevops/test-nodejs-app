def week = [1:'Sunday', 2:'Monday', 3:'Tuesday', 4:'Wednesday', 5:'Thursday', 6:'Friday', 7:'Saturday']
pipeline { 
	
  //environment {
    //week = "Mon"
  //  week = sh(returnStdout: true, script: 'date +%a')
    
  //}
   agent any
   stages {
   
      stage('Install Dependencies') { 
        steps { 
           sh 'echo "Install dependencies" '
          sh 'echo "${week}"'
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
         anyOf {
               branch 'prod'; branch 'release'
			   allOf {
                expression{env.BRANCH_NAME == 'develop'}
                expression{ week[new Date()[Calendar.DAY_OF_WEEK]] == 'Sunday' }
                 }
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
