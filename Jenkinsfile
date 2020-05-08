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
         docker.image('aquasec/trivy').withRun('--rm -v $WORKSPACE/cache:/root/.cache/ aquasec/trivy python:3.4-alpine') { c ->
    }
 
      }
  
//    stage('Pull-image-server') {
//         sh "docker-compose down"
//         sh "docker-compose up -d"	
//      }
}
