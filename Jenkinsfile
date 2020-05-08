pipeline {
	agent any
	
	environment {
	  
	  REPO = "webapp01"
	  ORGANIZATION = "p9sys"
 	}
    
    stages {
      
      stage ('Preparation') {
        steps {
      
          cleanWs()
          git url: "https://github.com/${ORGANIZATION}/${REPO}"


        }

      }


      stage ('Build') {
        steps {

          npm install	

        }







      }








    }






}