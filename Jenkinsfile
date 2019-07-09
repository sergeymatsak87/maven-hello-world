pipeline {
    agent {
        kubernetes {
          label 'maven_kube'
          defaultContainer 'jnlp'
          yaml """
              spec:
                  containers:
                  - name: maven
                    image: maven:3.3.9-jdk-8-alpine
                    command:
                    - cat
                    tty: true
                """
        }
    }
    stages {
        stage ('Build') {
            steps {            
                    echo "Run build..."
                    sh 'set'
                    container('maven') {
                        sh 'set'
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
