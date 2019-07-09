pipeline {
    agent any
    tools { 
       maven 'maven-3.6.1' 
       jdk 'jdk8' 
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
            }
        }
        stage ('Test') {
            steps {
                echo "Run test..."
                    sh 'mvn test'
            }
        }     
        stage ('Install') {
            steps {
                echo "Run install..."
                    sh 'mvn install'
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
