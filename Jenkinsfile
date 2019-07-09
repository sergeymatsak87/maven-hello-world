pipeline {
    agent {
        kubernetes {
          label 'maven_kube'
          containerTemplate {
            name 'maven'
            image 'maven:3.3.9-jdk-8-alpine'
            workingDir '/var/jenkins_home'
            ttyEnabled true
            command 'cat'
           }
        }
    }
    stages {
#        stage ('Initialize') {
#            steps {
#                container('jnlp') {
#                    sh 'echo "PATH = ${PATH}"'
#                    sh 'echo "M2_HOME = ${M2_HOME}"'
#                }
#            }
#        }
        stage ('Build') {
            steps {
                container('maven') {                
                    echo "Run build..."
                        sh 'mvn -f my-app/pom.xml clean package'
                        sh 'mvn -f my-app/pom.xml compile'
                        sh 'mvn -f my-app/pom.xml test'
                        sh 'mvn -f my-app/pom.xml install'
                }
            }
        } 
        stage ('Deploy') {
            steps {
                parallel (
                   a: {
                    echo "Deploy on Linux"
                   },
                   b: {
                    echo "Deploy on Windows"
                   }
                )
            }
        }
    }
}
