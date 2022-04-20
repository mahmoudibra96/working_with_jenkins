pipeline {
    agent any
    triggers {pollSCM('* * * * *')}


    stages {
        stage('Checkout') {
            steps {
                // Get some code from a GitHub repository
                git url: 'https://github.com/mahmoudibra96/spring-petclinic.git' , branch: 'main'
            }
        }
                
        stage('Build') {
            steps {
               
                // Run Maven on a Unix agent.
                sh "./mvnw clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
               
                always {
                 //   junit '**/target/surefire-reports/TEST-*.xml'
                 //   archiveArtifacts 'target/*.jar'
                //}
               // changed {
                    emailext attachLog: true,
                     body: 'please go to ${BUILD_NUMBER} and verify the build . ', 
                     compressLog: true,
                     recipientProviders: [buildUser()], 
                     subject: 'job\'${JOB_NAME}\'{${BUILD_NUMBER}} is waiting', 
                     to: 'test@localhost:8082'
                }
            }
        }
        
    }
}
