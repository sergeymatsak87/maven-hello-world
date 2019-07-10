podTemplate(label: 'mypod', containers: [
    containerTemplate(name: 'maven', image: 'maven:3.3.9-jdk-8-alpine', ttyEnabled: true, command: 'cat'),
    containerTemplate(name: 'jnlp', image: 'jenkins/jnlp-slave', args: '${computer.jnlpmac} ${computer.name}'),
]) {

    node ('mypod') {
        stage('Build a Maven project')
            container('maven') {
                sh 'mvn clean install'
            }
    }
}
