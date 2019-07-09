pipeline {
    agent {
        label 'jenkins_maven'
    }
    stages {
        stage ('compile') {
            steps {
                sh 'set'
                sh 'pwd'
                sh 'ls -la'
                sh 'mvn -f my-app/pom.xml clean compile test-compile'
            }
        }        
        stage ('unit test') {
            steps {
                sh 'mvn test'
            }
        }
        stage ('integration test') {
            steps {
                 sh 'mvn verify'
            }
        }
        stage ('install') {
            steps {
                 sh "mvn install"
            }
        }
        stage ('deploy to env') {
            when {
                expression {
                    branch == 'master'
                }
            }
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
