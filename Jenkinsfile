pipeline {
 agent any
 
 stages {
	stage('clone'){
		steps {
			echo 'Cloning source code'
			git branch:'main', url: 'https://github.com/guyn123/quanh.git'
		}
	} // end clone

        stage('restore package') {
		steps
		{
			echo 'Restore package'
			bat 'dotnet restore'
		}
	}
       stage ('build') {
		steps {
			echo 'build project netcore'
			bat 'dotnet build  --configuration Release'
		}
	}
       stage ('tests') {
		steps{
			echo 'running test...'
			bat 'dotnet test --no-build --verbosity normal'
		}
	}
       stage ('public den t thu muc')
	{
		steps{
			echo 'Publishing...'
			bat 'dotnet publish -c Release -o ./publish'
		}
	}
      
  stage ('Publish') {
		steps {
			echo 'public 2 runnig folder'
		//iisreset /stop // stop iis de ghi de file 
			bat 'xcopy "%WORKSPACE%\\publish" /E /Y /I /R "c:\\wwwroot\\WEBQUAN"'
 		}
	}

  stage('Deploy to IIS') {
            steps {
                powershell '''
               
                # Tạo website nếu chưa có
                Import-Module WebAdministration
                if (-not (Test-Path IIS:\\Sites\\WEBQUAN)) {
                    New-Website -Name "WEBQUAN" -Port 81 -PhysicalPath "c:\\wwwroot\\WEBQUAN"
                }
                '''
            }
        } // end deploy iis

  } // end stages
}//end pipeline

