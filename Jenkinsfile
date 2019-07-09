pipeline {
    agent {
        kubernetes {
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
                    bash 'mvn clean'
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
