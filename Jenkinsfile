def label = 'jenkins_slave_maven'

  podTemplate(label: label, yaml: """
    apiVersion: v1
    kind: Pod
    spec:
      serviceAccountName: jenkins
      containers:
      - name: maven
        command:
        - cat
        tty: true
        env:
        - name: _JAVA_OPTIONS
          value: -Xmx300M
        image: maven:3.6.1-jdk-8
        """) {

    node(label) {
      stage('Package') {
          container('maven') {
            sh 'mvn clean compile test-compile install'
          }
        }
      }
    }
