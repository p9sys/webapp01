pipeline {
	agent any
	
	environment {

	  	GITHUB_ORGANIZATION = "p9sys"
	  	GITHUB_REPO = "webapp01"
	  	DOCKERHUB_REGISTRY = "pf9sys/webapp01"
 	}
    
    stages {
      
    	stage ('PREPARATION') {
        	steps {
      
          		cleanWs()
          		git url: "https://github.com/${GITHUB_ORGANIZATION}/${GITHUB_REPO}"
	        }
	    }


      	stage ('BUILD') {
        	steps {

          		sh 'npm install'

        	}
        }	

        Stage ('PUBLISH') {
        	environment {
           
            	registryCredential = 'dockerhub'
          	}
          	steps {

               	 	script {
                    	def appimage = docker.build DOCKERHUB_REGISTRY + ":$BUILD_NUMBER"
                    	docker.withRegistry( '', registryCredential ) {
                        	appimage.push()
                        	appimage.push('latest')
                    	}
              	  	}

          	}

        }

        Stage ('DEPLOY') {
        	steps {

        		sh 'kubectl apply -f k8s/app.yaml'
        	}
        }
    }
}