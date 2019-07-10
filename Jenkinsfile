podTemplate(label: 'mypod', containers: [
    containerTemplate(name: 'maven', image: 'jenkins-slave-maven-rhel7', ttyEnabled: true, command: 'cat'),
]) {

    node ('mypod') {
            stage 'Build a Maven project'
            sh 'mvn clean install'
    }
}
