rtServer (
    id: 'Artifactory-1',
    url: 'http://my-artifactory-domain/artifactory',
    // If you're using username and password:
    username: 'user',
    password: 'password'
    // If you're using Credentials ID:
    credentialsId: 'ccrreeddeennttiiaall'
    // If Jenkins is configured to use an http proxy, you can bypass the proxy when using this Artifactory server:
    bypassProxy: true
    // Configure the connection timeout (in seconds).
    // The default value (if not configured) is 300 seconds:
    timeout = 300
)
pipeline {
    agent {
        node {
        label 'slave'
        }
    }
    tools {
        maven 'Maven 3.3.9'
        jdk 'jdk8'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh 'echo hello world'
            }
        }
    }
}
