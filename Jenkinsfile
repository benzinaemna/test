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
        sh 'sudo docker build -t emnabenzina/testangular .'
    }
}
    stage ('DockerHub Push') {
    steps {
        withCredentials([string(credentialsId: 'emnabenzina', variable: 'dockerHubPwd')]) {
            sh "sudo docker login -u emnabenzina -p ${dockerHubPwd}"
}
         sh "sudo docker push emnabenzina/testangular"

}
}
    stage ('Deploy') {
    steps{
        sshagent(credentials: ['emnab']) {
        sh "ssh vagrant@10.10.0.233"
//sh "scp target/hello-world-app-1.0-SNAPSHOT.jar vagrant@192.168.1.201:/home/vagrant"
        sh "ssh vagrant@10.10.0.233 'docker run image_name:${DOCKER_TAG}'"
}
}
}
}
}
def getVersion() {
    def version = sh returnStdout: true, script: 'git rev-parse --short HEAD'
    return version.trim()
}
