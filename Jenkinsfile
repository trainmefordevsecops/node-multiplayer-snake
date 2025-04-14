node ('docker-host-server'){
    def app
    stage('Cloning Git') {
        /* Let's make sure we have the repository cloned to our workspace */
       checkout scm
    }  
    stage('SAST'){
        build 'SECURITY-SAST-SNYK'
    }

    
    stage('Build-and-Tag') {
    /* This builds the actual image; synonymous to
         * docker build on the command line */
        app = docker.build("bruno101/snake")
    }
    stage('Post-to-dockerhub') {
    
     docker.withRegistry('https://registry.hub.docker.com', 'train_creds') {
            app.push("latest")
        			}
         }
    stage('SECURITY-IMAGE-SCANNER'){
        build 'SECURITY-IMAGE-SCANNER-AQUAMICROSCANNER'
    }
  
    
    stage('Pull-image-server') {
    
         sh "docker-compose down"
         sh "docker-compose up -d"	
      }
    
    stage('DAST')
        {
        build 'SECURITY-DAST-OWASP_ZAP'
        }
 
}
