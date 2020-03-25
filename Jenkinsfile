pipeline {
   agent any

   tools {
      // Install the Maven version configured as "M3" and add it to the path.
      maven "maven-3.6.3"
   }

   stages {
      stage('Git fetch') {
         steps {
            // Get some code from a GitHub repository
            git 'https://github.com/spring-projects/spring-petclinic.git'
         }
      }
      stage('Compile') {
         steps {
      
            // Run Maven on a Unix agent.
            sh "mvn clean package"

         }
      }
      stage('Test') {
         steps {
      
            // Run Maven on a Unix agent.
            sh "mvn test"

         }

         post {
            // If Maven was able to run the tests, even if some of the test
            // failed, record the test results and archive the jar file.
            success {
               junit '**/target/surefire-reports/TEST-*.xml'
               archiveArtifacts 'target/*.jar'
            }
         }
      }
      stage('Package') {
         steps {
      
            // Run Maven on a Unix agent.
            sh "mvn package"

         }
      }
   }
}
