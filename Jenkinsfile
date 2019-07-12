pipeline {
  agent {
    label "maven"
    kubernetes {
      yamlFile 'KubernetesPod.yaml'
    }
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
