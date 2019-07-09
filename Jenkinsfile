pipeline {
    agent {
        kubernetes {
          name 'jenkins-maven-slave'
          label 'maven_kube'
          containerTemplate {
            name 'maven'
            image 'maven:3.3.9-jdk-8-alpine'
            workingDir '/home/jenkins'
            ttyEnabled true
            command 'cat'
           }
        }
    }
    stages {
        stage ('Build') {
            steps {            
                    echo "Run build..."
                    sh 'set'
                    container('maven') {
                        sh 'mvn -version'
                        sh 'mvn clean'
                        sh 'mvn compile'
                        sh 'mvn install'
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
