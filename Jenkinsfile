pipeline {
  agent {
    kubernetes {
      yamlFile 'KubernetesPod.yaml'
    }
  }
  options {
    // Because there's no way for the container to actually get at the git repo on the disk of the box we're running on.
    skipDefaultCheckout(true)
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
