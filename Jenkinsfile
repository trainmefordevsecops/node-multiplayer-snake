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
         sh "export VERSION=0.6.0"
         sh "echo $VERSION"
         sh "wget https://github.com/aquasecurity/trivy/releases/download/v${VERSION}/trivy_${VERSION}_Linux-64bit.tar.gz"
         
 
      }
  
//    stage('Pull-image-server') {
//         sh "docker-compose down"
//         sh "docker-compose up -d"	
//      }
}
