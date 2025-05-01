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
                git branch: 'main', url: 'https://github.com/edwin-ainikkal/jenkins-hello-world.git'
                // Add other build steps here
                sh "mvn clean package -DskipTests=true"
            }
        }
        stage('Unit Test') {
            steps {
                sh "mvn test"
                junit stdioRetention: '', testResults: 'target/surefire-reports/TEST-*.xml'
            }
        }
        stage('Integration Testing') {
            steps {
                sh "sleep ${params.SLEEP_TIMER}"
                sh "curl -v http://localhost:${params.APPLICATION_PORT}/hello"
                sh """
                    RESPONSE=\$(curl -s http://localhost:${params.APPLICATION_PORT}/hello)
                    echo "Response: \$RESPONSE"
                    echo "\$RESPONSE" | grep -i "Hello, KodeKloud community!" || echo "Expected response not found"
                """

            }
        }

        
    }
}
