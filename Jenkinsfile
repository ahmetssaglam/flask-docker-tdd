pipeline {
    agent any

    stages {
        stage('build') {
            steps {
		    script {
		    	try {
		        	sh 'nc -vz 127.0.0.1 5000'
		        	echo 'Docker already up !'
	            	}
	            	catch (err) {
	 	        	echo 'Building started !'
		        	sh 'docker-compose up -d'
	            	}
		    }
            }
        }
	stage('preparation-test') {
	    steps {
		sh 'docker exec tdd-web pip3 install pytest'
		echo 'Pytest Installed !'
	    }
	}
	stage('test') {
	    steps {
		echo 'Waiting for DB !!'
		// sh 'sleep 30'	
		script {
			try {
				sh 'docker exec tdd-web python3 -m pytest tests'
				echo 'Test Passed !'
			}
			catch (err) {
				
				echo 'commmmmit'
				//git url: "git@github.com:ahmetssaglam/flask-docker-tdd.git",
				   // credentialsId: 'bdefd814-cf0d-4e6d-8a6a-08b00bd71ab1',
				  //  branch: 'dev'
				//sh 'git remote remove origin'
				//sh 'git remote add origin https://ahmetssaglam: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@github.com/ahmetssaglam/flask-docker-tdd.git'
				
				
				
				
				sh 'git checkout dev'
				sh 'git reset --hard c34b3a638f70c9caa9a5f8eb867e77db3408b3a6'
				// sh 'git reset --hard dev@{1.minutes.ago}'
				// sh 'git reset --hard HEAD~1'
				//sh 'git push -f origin dev'
				
				
				withCredentials([usernamePassword(credentialsId: '544c6976-c5bb-4725-ba89-1e51b55a5e61', passwordVariable: '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', usernameVariable: 'ahmetssaglam')]) {
                        		sh('git push -f https://ahmetssaglam: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@github.com/ahmetssaglam/flask-docker-tdd.git')
                  		  }

				
				
				echo 'Test Failed ! Changes Reverted !'
			}
		}
		echo 'Test Completed !'
	    }
	}
    }
}
