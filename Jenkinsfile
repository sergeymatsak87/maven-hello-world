pipeline {
  agent any
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
