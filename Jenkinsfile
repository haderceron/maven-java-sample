pipeline {
    agent any
    tools { 
        maven 'maven3.6.0' 
        jdk 'sapmachine-jdk-12.0.1.jdk' 
    }
    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/haderceron/maven-java-sample.git'

                // Run Maven on a Unix agent.
                sh "./mvnw clean install -Dcheckstyle.skip"
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
    }
}
