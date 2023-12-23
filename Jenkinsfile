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
        sh 'docker build -t emnabenzina/testangular .'
    }
}
    stage ('DockerHub Push') {
    steps {
        withCredentials([string(credentialsId: 'emnabenzina', variable: 'dockerHubPwd')]) {
            sh "docker login -u emnabenzina -p ${dockerHubPwd}"
}
         sh "docker push emnabenzina/testangular"

}
}
  stage ('Pre_Deploy') {
    sh "ssh -t -t vagrant@10.10.0.145"
  }
    stage ('Deploy') {
    steps{
        sshagent(credentials: ['Vagrant_ssh']) {
        sh "ssh -t -t vagrant@10.10.0.145"
//sh "scp target/hello-world-app-1.0-SNAPSHOT.jar vagrant@192.168.1.201:/home/vagrant"
        sh "ssh vagrant@10.10.0.145 'docker run image_name:${DOCKER_TAG}'"
}
}
}
}
}
def getVersion() {
    def version = sh returnStdout: true, script: 'git rev-parse --short HEAD'
    return version.trim()
}
