pipeline {
    agent { label 'linuxnode' }
    
    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "MVN3"
        jdk "JDK8"
    }

    stages {
        stage("Ennable webhook") {
            steps {
                script {
                    properties([pipelineTriggers([githubPush()])])
                }
            }
        }
        
        stage('pullscm') {
            steps {
                git credentialsId: 'github-credential', url: 'git@github.com:Saneesh/jenkins_test.git'
            }
        }
        
        stage("print") {
            steps {
                echo "printing some thing"
            }
        }
        stage('Build') {
            steps {
                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true -f api-gateway clean package"

                // To run Maven on a Windows agent, use
                //bat "mvn -Dmaven.test.failure.ignore=true -f api-gateway clean package"
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
