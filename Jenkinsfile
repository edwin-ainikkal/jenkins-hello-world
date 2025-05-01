pipeline {
    agent any
    tools {
        // Install the Maven version configured as "maven-398" and add it to the path.
        maven "maven-398"
    }
    stages {
        stage('Build') {
            steps {
                // Get some code from a Git repository
                git 'https://github.com/edwin-ainikkal/jenkins-hello-world.git'
                // Add other build steps here
            }
        }
        stage('Unit Test') {
            steps {
                sh "mvn test"
                junit stdioRetention: '', testResults: 'target/surefire-reports/TEST-*.xml'
            }
        }
        
    }
}
