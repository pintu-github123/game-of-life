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
	    pollSCM('*/5 * * * *')
        }
     
        parameters { 
	      choice(name: 'GOAL', choices: ['compile', 'package', 'clean package']) 
	}


        stages{
              stage( 'SourceCode' ){
                    steps{
                         git branch: 'dev', credentialsId: 'jenkins-28022022', url: 'https://github.com/pintu-github123/game-of-life.git'
			 //input message: 'Continue to the next stage?',submitter: 'jenkins'
			 //https://www.jenkins.io/doc/book/pipeline/syntax/#input
                    }
              }
             stage('Build the Source Code'){
                    steps{
                        sh " mvn ${params.GOAL} " 
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

       
        post{
	    //https://www.jenkins.io/doc/book/pipeline/syntax/#post
            always{
	        //https://www.jenkins.io/doc/pipeline/steps/workflow-basic-steps/#mail-mail
                mail from: "devops@qt.com",
                to: 'team@qt.com',
                subject: "Status of the pipeline ${currentBuild.fullDisplayName}",
                body: "${env.BUILD_URL} has a result ${currentBuild.result}"
	    }
	}
}    

