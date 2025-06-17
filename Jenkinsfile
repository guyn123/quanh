pipeline {
 agent any
 
 stages {
	stage('clone'){
		steps {
			echo 'Cloning source code'
			git branch:'main', url: 'https://github.com/guyn123/quanh.git'
		}
	} // end clone

  } // end stages
}//end pipeline
