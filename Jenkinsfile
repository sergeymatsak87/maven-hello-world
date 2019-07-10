def label = UUID.randomUUID().toString()

  podTemplate(label: label, yaml: """
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: maven
    command:
    - cat
    tty: true
    env:
    - name: BUILD_NUMBER
      value: ${env.BUILD_NUMBER}
    - name: BRANCH_NAME
      value: ${env.BRANCH_NAME}
    - name: _JAVA_OPTIONS
      value: -Xmx300M
    image: maven:3.6.1-jdk-8
    resources:
      limits:
        memory: 1500Mi
      requests:
        cpu: 100m
        memory: 1500Mi
    """) {

    node(label) {
      stage('Package') {
        try {
          container('maven') {
            sh 'mvn clean compile test-compile install -Dmaven.test.skip=true'
          }
        }
      }
      stage('Test') {
        try {
          container('maven') {
            sh 'mvn -B -ntp test -DconnectorHost=0.0.0.0'
          }
        } finally {
          junit '**/target/surefire-reports/**/*.xml'
        }
      }
    }
  }
