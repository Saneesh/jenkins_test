pipeline {
    agent {
        label 'windows'
    }
    
    tools {
        // Install the Maven version configured as "M3" and add it to the  path.
        maven "MVN3"
        jdk "jdk8"
    }

    stages {
        stage('pullscm') {
            steps {
                git credentialsId: 'GitHub', url: 'git@github.com:Saneesh/jenkins_test.git'
            }
        }
        
                
        stage('Build') {
            steps {
                // Run Maven on a Unix agent.
                // sh "mvn -Dmaven.test.failure.ignore=true -f api-gateway clean package"

                // To run Maven on a Windows agent, use
                bat "mvn -Dmaven.test.failure.ignore=true -f api-gateway clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit 'api-gateway/target/surefire-reports/*.xml'
                    archiveArtifacts 'api-gateway/target/*.jar'
                }
            }
        }
    }
}
