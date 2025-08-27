pipeline {
    agent any // Run on any available agent

    tools {
        jdk 'JDK-21'
        maven 'maven-3.9.11' // 1. Ensure a Maven tool named 'maven-3.9.6' is configured in Jenkins
    }

    stages {
        stage('Build') {
            steps {
                // 2. Run the Maven command to compile and package the application
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                // 3. Run the Maven command to execute the tests
                sh 'mvn test'
            }
            post { // 4. Actions to run after the stage completes
                always {
                    // 5. Archive the test results for display in Jenkins
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                echo 'Delivering the application...'
                // In a real scenario, you might publish to a repository here
                // For now, we'll archive the final application file
                archiveArtifacts 'target/*.jar'
            }
        }
    }
}
