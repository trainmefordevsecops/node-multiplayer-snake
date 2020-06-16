node ('appserver'){  
    def app
    stage('Cloning Git') {
       checkout scm
    }  
    
 stage('Build-and-Tag') {
       app = docker.build("mikebroomfield/snake")
   }
    
    stage('Post-to-dockerhub') {
     docker.withRegistry('https://registry.hub.docker.com') {
            app.push("latest")
        			}
         }
    
     stage('Trivy Scan') {
         """
         sh "./trivy --no-progress --exit-code 0 --severity HIGH,CRITICAL python:3.4-alpine"
         """
 
      }
  
    stage('Pull-image-server') {
         sh "docker-compose down"
         sh "docker-compose up -d"	
      }

}
