pipeline {
    agent any
    stages {
        stage('build') {
                steps {
                        echo 'Running the build or build code...'
			
                }
        }
	    stage('test: integration-&-quality'){
		    
		steps {
			input('Do you want to proceed?')
        }
	    }
        stage('test: functional') {
                
                steps {
			echo "Running the functional test..."
                        }
        }
        stage('test: load-&-security') {
                parallel {
                        stage('performance Test') {
                                steps{
                                        echo "Running the performance test..."
                                }
                        }
                        stage('Integration test') {
                        
				steps {
					echo 'Running the integration test..'
				}
                               
			}  }
        }
        stage('approval') {
                
                steps {
			echo "Running the approval process"
                        }
        }
        stage('deploy:prod') {
                
                steps {
			echo "Running the deployment in prod process"
                        }
        }
    }
}
