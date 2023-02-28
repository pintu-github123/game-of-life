node ('JDK-8'){

           stage('SourceCode'){
            // Clone the Project from Git-Hub
            git branch: 'dev', 
            credentialsId: 'jenkins-28022022', 
            url: 'https://github.com/pintu-github123/game-of-life.git'
          }

           stage('Build the Source Code'){
           //Build the Source Code
           sh 'mvn clean package'
          }

          stage('Archive The Artifact'){
            // Archive the artifact
           archiveArtifacts artifacts: '**/*.war', followSymlinks: false
         }

         stage('Publish the JUNIT Test Results'){
           junit '**/surefire-reports/*.xml'
        }
}
