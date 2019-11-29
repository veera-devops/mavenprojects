pipeline {
   agent any

   stages {
      stage('Build') {
         steps {
            // Get some code from a GitHub repository
            git 'https://github.com/veera-devops/mavenprojects.git'

            // Run Maven on a Unix agent.
            sh '''
            cd om
            mvn clean install
            '''
              }

         post {
            // If Maven was able to run the tests, even if some of the test
            // failed, record the test results and archive the jar file.
            success {
               sh '''
               cp -r /var/lib/jenkins/workspace/pipelinejobformavenbuild/om/target/om.war /apps/jarbackup
               '''
            }
            always{
               emailext body: 'Test Results: pipeline script for maven build', 
               subject: 'Maven Build', 
               to: 'devopsveerav@gmail.com' 
            }
         }
      }
   }
}
