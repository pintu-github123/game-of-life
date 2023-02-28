pipeline{

        agent{ label 'JDK-8'}
        
        environment{
            PATH = "/opt/apache-maven-3.9.0/bin:$PATH"
        }
        
	 options { 
             timeout(time: 1, unit: 'HOURS')
             retry(2)  //// if build failure plz retry it 
        }
	
        triggers {
            cron('0 * * * *') ////Build periodically every one hour
        }

        stages{
              stage( 'SourceCode' ){
                    steps{
                         git branch: 'master', credentialsId: 'jenkins-28022022', url: 'https://github.com/pintu-github123/game-of-life.git'
                    }
              }
             stage('Build the Source Code'){
                    steps{
                        sh 'mvn clean package '
                    }
             }
             stage('Archive The Artifact'){
                    steps{
                          archiveArtifacts artifacts: '**/*.war', followSymlinks: false
                    }
             }
             stage('Publish the JUNIT Test Results'){
                   steps{
                        junit '**/surefire-reports/*.xml'
                   }
             }
        
       }

       post {
        success {
            // send the success email
            mail bcc: '', body: 'Build Successfull', cc: 'sksahoo2007@gmail.com', from: 'TCS World bank Project', replyTo: '', 
	    subject: 'game-of-line Pipeline Project', to: 'subhrak.sahoo@gmail.com'
            echo "$BRANCH_NAME branch Successfull executed with Build N0 - $BUILD_NUMBER"
        }
        unsuccessful {
            //send the unsuccess email
            echo "failure"
        }
    }
        
}    

