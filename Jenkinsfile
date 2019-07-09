pipeline {
    agent {
       label "maven_kube"
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
                parallel {
                   a: {
                    echo "Build on Linux"
                    sh 'mvn -Dmaven.test.failure.ignore=true install'
                   },
                   b: {
                    echo "Build on Windows"
                    sh 'mvn -Dmaven.test.failure.ignore=true install'
                   }
                }
            }
            post {
                success {
                    junit 'target/surefire-reports/**/*.xml' 
                }
            }
        }
    }
}
