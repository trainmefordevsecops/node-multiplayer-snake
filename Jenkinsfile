node ('appserver'){  
    def app
    stage('Cloning Git') {
       checkout scm
    }  
    
    stage('Running Snyk') {
   snykSecurity failOnIssues: false, snykInstallation: 'SnykV2PluginTest', snykTokenId: 'snyktoken'
     } 
    
    stage('Build-and-Tag') {
        app = docker.build("mikebroomfield/snake")
    }
    
    stage('Post-to-dockerhub') {
     docker.withRegistry('https://registry.hub.docker.com', 'dockercreds') {
            app.push("latest")
        			}
         }
    
     stage('Trivy Scan') {
         sh "VERSION=$(
         curl --silent "https://api.github.com/repos/aquasecurity/trivy/releases/latest" | \
         grep '"tag_name":' | \
         sed -E 's/.*"v([^"]+)".*/\1/'
         )"
         sh "echo $VERSION"	
      }
  
    stage('Pull-image-server') {
         sh "docker-compose down"
         sh "docker-compose up -d"	
      }
}
