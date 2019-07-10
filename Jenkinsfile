pipeline {
  agent {
    label 'jnlp_jenkins_slave'
  }
  stages {
    stage('Run maven') {
      steps {
        sh 'set'
        container('maven') {	
          sh 'mvn -version'	
        }
      }
    }
  }
}
