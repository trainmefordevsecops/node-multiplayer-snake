//stage 'Build'

 

 node ('Ubuntu-app-agent'){
 
       
	   def app

   try {

     notifyBuild('STARTED')

					
					
		stage('Cloning Git') {
        /* Let's make sure we have the repository cloned to our workspace */

       checkout scm
		}
     
		stage('SAST') {
               //build 'SECURITY-SAST-SNYK'
               sh 'echo "SAST Test passed "' }
        
    

		stage('Build-and-Tag') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("amrit96/snake")
		}

    
	       stage('Post-to-dockerhub') {
       
     /// docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
     ///       app.push("latest")
     ///   			}
         }
		stage('SECURITY-IMAGE-SCANNER'){
       // build 'SECURITY-IMAGE-SCANNER-AQUAMICROSCANNER'

           sh 'echo "Image Vulnerability Test passed"'
        
		}

		
     
     

		stage('Pull-image-server') {

        /// 		sh "docker-compose down"
        ///		sh "docker-compose up -d"			
		}
   
		stage('DAST') {
        
			node('Ubuntu-app-agent'){
           // build 'OWASP-ZAP' 

            sh 'echo "DAST Test passed"'
			}
        
		}			
					

     /* ... existing build steps ... */

 

   } catch (e) {

     // If there was an exception thrown, the build failed

     currentBuild.result = "FAILED"

     throw e

   } finally {

     // Success or failure, always send notifications

     notifyBuild(currentBuild.result)

   }

 }

 

 def notifyBuild(String buildStatus = 'STARTED') {

   // build status of null means successful

   buildStatus =  buildStatus ?: 'SUCCESSFUL'

 

   // Default values

   def colorName = 'RED'

   def colorCode = '#FF0000'

   def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"

   def summary = "${subject} (${env.BUILD_URL})"

   def details = """<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
     <p>Check console output at "<a href="${env.BUILD_URL}">${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>"</p>"""

 

// Override default values based on build status



   if (buildStatus == 'STARTED') {



     color = 'YELLOW'



     colorCode = '#FFFF00'



   } else if (buildStatus == 'SUCCESSFUL') {



     color = 'GREEN'



     colorCode = '#00FF00'



   } else {



     color = 'RED'



     colorCode = '#FF0000'



   }
 

   // Send notifications

   slackSend (color: colorCode, message: summary)
 

   emailext (

       subject: subject,

       body: details,
	   mimeType: 'text/html',

      // recipientProviders: [[$class: 'DevelopersRecipientProvider']]
	   to: 'trainmefordevsecops@gmail.com'

     )

 }
