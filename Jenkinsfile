def week = [1:'Sunday', 2:'Monday', 3:'Tuesday', 4:'Wednesday', 5:'Thursday', 6:'Friday', 7:'Saturday']

pipeline 
{ 
		triggers 
		{
			cron(env.BRANCH_NAME == 'develop' ? '0 11 29 09 4' : '')
  		}
		agent any
		options 
		{
			buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '3', numToKeepStr: '3')
		}
		stages 
		{
			stage('Install Dependencies') 
			{ 
				steps 
				{ 
					sh 'echo "Install dependencies" '
					sh 'echo Branch is:' + env.BRANCH_NAME
				}
			}
     
			stage('Test') 
			{
				when 
				{
					beforeAgent true
					anyOf 
					{
						branch 'prod'; branch 'release'
						allOf 
						{
							expression{env.BRANCH_NAME == 'develop'}
							expression{ week[new Date()[Calendar.DAY_OF_WEEK]] == 'Thursday' }
						}
					}
				}
				steps 
				{ 
					sh 'echo "testing application..."'
				}
			}
			
			stage("Deploy application") 
			{ 
				steps 
				{ 
					sh 'echo "deploying application..."'
				}

			}
     	}
}
