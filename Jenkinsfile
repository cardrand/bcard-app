
node('maven-label') {
   def mvnHome
   stage('Preparation') { // for display purposes
       git 'https://github.com/cardrand/bcard-app.git'
      mvnHome = tool 'maven'
   }
   stage('Build') {
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package sonar:sonar -Dsonar.host.url=http://ip-172-31-28-31.ap-south-1.compute.internal:9000/'
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
