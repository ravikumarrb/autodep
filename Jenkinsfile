node {
   def mvnHome
   stage('get the code') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/codepipe/autodep.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'M3'
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('test') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.jar'
   }
   
   stage ('install') {
      bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package install/)
	  }
}
