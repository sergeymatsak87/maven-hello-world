pipeline {
    agent {
        kubernetes {
            label 'jenkins_slave_maven'
            defaultContainer 'jnlp'
        }
    }
    stages {        
        stage ('compile') {
            steps {
                sh 'set'
                sh 'pwd'
                sh 'ls -la'
                container('jnlp') {
                    sh 'pwd'
                    sh 'mvn -f my-app/pom.xml clean compile test-compile'
                }
            }
        }        
        stage ('unit test') {
            steps {
                container('maven') {
                    sh 'mvn test'
                }
            }
        }
        stage ('integration test') {
            steps {
                container ('maven') {
                    sh 'mvn verify'
                }
            }
        }
        stage ('install') {
            steps {
                container('maven') {
                    sh "mvn install"
                }
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
