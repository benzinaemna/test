pipeline {
agent any
environment {
  def DOCKER_TAG = getVersion()
}
stages {
stage ('Clone Stage') {
steps {
    git branch:'main',url:'https://github.com/benzinaemna/test.git'
}
}
stage ('Docker Build') {
    steps {
        bat 'docker build -t emnabenzina/testangular .'
    }
}
    stage ('DockerHub Push') {
    steps {
        withCredentials([string(credentialsId: 'emnabenzina', variable: 'dockerHubPwd')]) {
            bat "docker login -u emnabenzina -p ${dockerHubPwd}"
}
         bat "docker push emnabenzina/testangular"

}
}
    stage ('Deploy') {
    steps{
        sshagent(credentials: ['Vagrant_ssh']) {
        bat "ssh user@172.17.0.1"
//sh "scp target/hello-world-app-1.0-SNAPSHOT.jar vagrant@192.168.1.201:/home/vagrant"
        bat "ssh user@172.17.0.1 'docker run "image_name:${DOCKER_TAG}"'"
}
}
}
}
}
def getVersion() {
    def version = bat returnStdout: true, script: 'git rev-parse --short HEAD'
    return version.trim()
}
