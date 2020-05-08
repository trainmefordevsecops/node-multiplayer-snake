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
        
       sh "apt-get install wget apt-transport-https gnupg"
       sh "wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | apt-key add -"
       sh "echo deb https://aquasecurity.github.io/trivy-repo/deb bionic main | tee -a /etc/apt/sources.list.d/trivy.list"
       sh "apt-get update"
       sh "apt-get install -y trivy"
       sh "trivy --help"
         
 
      }
  
    stage('Pull-image-server') {
         sh "docker-compose down"
         sh "docker-compose up -d"	
      }
}
