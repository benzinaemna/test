pipeline {
agent any
environment {
   DOCKER_TAG = getVersion()
}
stages {
stage ('Clone Stage') {
steps {
    git "https://github.com/benzinaemna/test.git"
}
}
stage ('Docker Build') {
    steps (
        sh'docker build -t emnabenzina/testAngular:'+${DOCKER_TAG}+'.'
    }
}
stage ('DockerHub Push') {
    steps {
        withCredentials([string(credentialsId: 'emnabenzina', variable: 'dockerHubPwd')]) {
            sh "sudo docker login -u emnabenzina -p ${DockerHubPassword}"
        }
        sh "sudo docker push emnabenzina/testAngular:${DOCKER_TAG}"
}
}

}
}
def getVersion(){
    def version = sh returnStdout: true,script: "git rev-parse --short HEAD"
    return version
}
