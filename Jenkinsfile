@Library('pipeline-library-demo')_

node ("maven-slave"){
   def mvnHome
   stage('testLibrary') {
      echo 'Hello Demo World'

      sayHello 'Dave'
   }
   
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/bunty2019/xcard.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'mymaven'
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
   }
}
