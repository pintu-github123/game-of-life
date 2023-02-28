pipeline{

        agent{ label 'JDK-8'}
        
        environment{
        PATH = "/opt/apache-maven-3.9.0/bin:$PATH"
        }
        
        stages{
              stage( 'SourceCode' ){
                    steps{
                         git branch: 'master', credentialsId: 'jenkins-28022022', url: 'https://github.com/pintu-github123/game-of-life.git'
                    }
              }
             stage('Build the Source Code'){
                    steps{
                        sh 'mvn clean package'
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
        
}    

