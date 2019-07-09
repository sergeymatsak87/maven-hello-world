properties([
        parameters(
                [
                        booleanParam(
                                name: 'DEPLOY_BRANCH_TO_TST',
                                defaultValue: false
                        )
                ]
        )
])

def branch
def revision
def registryIp

pipeline {

    agent {
        kubernetes {
            label 'jenkins_slave_maven'
            defaultContainer 'jnlp'
            yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    job: build-maven
spec:
  containers:
  - name: maven
    image: maven:3.6.0-jdk-11-slim
    command: ["cat"]
    tty: true
"""
        }
    }

    stages {
        stage ('checkout') {
            steps {
                script {
                    def repo = checkout scm
                    revision = sh(script: 'git log -1 --format=\'%h.%ad\' --date=format:%Y%m%d-%H%M | cat', returnStdout: true).trim()
                    branch = repo.GIT_BRANCH.take(20).replaceAll('/', '_')
                    if (branch != 'master') {
                        revision += "-${branch}"
                    }
                    sh "echo 'Building revision: ${revision}'"
                }
            }

        }        
        stage ('compile') {
            steps {
                container('maven') {
                    sh 'mvn clean compile test-compile'
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
