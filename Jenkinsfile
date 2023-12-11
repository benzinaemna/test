pipeline {
agent any
tools{ jdk 'java17' }
environment {
   DOCKER_TAG = getVersion()
}
stages {
stage ('Clone Stage') {
steps {
    git 'https://github.com/benzinaemna/test.git'
}
}
stage ('Docker Build') {
    steps {
        bat 'docker build -t emnabenzina/image_name:${DOCKER_TAG}.'
    }
}
stage ('DockerHub Push') {
    steps {
        withCredentials([string(credentialsId: 'emnabenzina', variable: 'dockerHubPwd')]) {
            bat 'docker login -u emnabenzina -p ${DockerHubPassword}'
        }
        bat 'docker push emnabenzina/image_name:${DOCKER_TAG}'
}
}

}
}
def getVersion(){
    def version = bat returnStdout: true,script: 'git rev-parse --short HEAD'
    return version
}
