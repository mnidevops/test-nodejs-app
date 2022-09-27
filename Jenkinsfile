def week = [1:'Sunday', 2:'Monday', 3:'Tuesday', 4:'Wednesday', 5:'Thursday', 6:'Friday', 7:'Saturday']
//cron_string = BRANCH_NAME == "develop" ? 46 22 27 9 * : ""

pipeline { 
	triggers {
		cron(env.BRANCH_NAME == 'develop' ? '1 * * * *' : '')
		//cron(env.BRANCH_NAME = 'develop' ? '40 22 27 9 *' : '')
      		//cron(cron_string)
  		}
	//environment {
	//	brch= 'env.BRANCH_NAME'
	//}
   agent any
	options {
  buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '3', numToKeepStr: '3')
}
   stages {
   	
      stage('Install Dependencies') { 
        steps { 
           	sh 'echo "Install dependencies" '
		//sh 'printenv'
		sh 'echo Branch is:' + env.BRANCH_NAME
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
                expression{ week[new Date()[Calendar.DAY_OF_WEEK]] == 'Tuesday' }
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
