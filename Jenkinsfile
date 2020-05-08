node ('appserver'){  
    def app
    stage('Cloning Git') {
       checkout scm
    }  
    
   // stage('Running Snyk') {
  // snykSecurity failOnIssues: false, snykInstallation: 'SnykV2PluginTest', snykTokenId: 'snyktoken'
  //   } 
    
 //stage('Build-and-Tag') {
 //      app = docker.build("mikebroomfield/snake")
 //  }
    
 //   stage('Post-to-dockerhub') {
  //   docker.withRegistry('https://registry.hub.docker.com', 'dockercreds') {
 //           app.push("latest")
 //       			}
 //        }
    
     stage('Trivy Scan') {
         sh "wget https://github.com/aquasecurity/trivy/releases/download/v0.6.0/trivy_0.6.0_Linux-64bit.tar.gz"
         sh "tar -zxvf trivy_0.6.0_Linux-64bit.tar.gz"
         sh "./trivy --no-progress --exit-code 1 --severity HIGH,CRITICAL mikebroomfield/snake
         
 
      }
  
//    stage('Pull-image-server') {
//         sh "docker-compose down"
//         sh "docker-compose up -d"	
//      }
}
