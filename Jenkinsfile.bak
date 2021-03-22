node {
   def mvnHome

   
	
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      // git 'https://github.com/denisptech/spring-petclinic.git'
      git branch: 'main', url: 'https://github.com/denisptech/spring-petclinic.git'
      // Get the Maven tool.
      // ** NOTE: This 'Maven3.6.3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'maven-3.6.3'
   }
   stage('Build') {
      // Run the maven build
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
         }
      }
   }
   stage('Results') {

      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
	
   }
}