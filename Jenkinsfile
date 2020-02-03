// ZedOps
//This JenkinsFile requires a Slave , Tool Configuration && a Jfrog Artifactory Server
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
        stage('upload') {
            steps {
               script { 
                  def server = Artifactory.server 'zedops'
                  def uploadSpec = """{
                     "files": [{
                        "pattern": "target/my-app*.jar",
                        "target": "gradle-dev-local/zedops/my-app.jar"
                     }]
                  }"""

                  server.upload(uploadSpec)
               }
            }
        }
    }
}
