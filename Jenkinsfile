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
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }
        stage ('Build') {
            steps {
                echo "Run build..."
                    sh 'mvn clean package'
                    sh 'mvn compile'
                    sh 'mvn test'
                    sh 'mvn install[
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
