pipeline {
agent any
environment {
   DOCKER_TAG = getVersion()
}
stages {
stage ('Clone Stage') {
steps {
    git branch:'main',url:'https://github.com/benzinaemna/test.git'
}
}
stage ('Docker Build') {
    steps {
      bat 'echo ${DOCKER_TAG}'
        bat 'docker build -t emnabenzina/DataCamp:${DOCKER_TAG} .'
    }
}
    stage ('DockerHub Push') {
    steps {
        withCredentials([string(credentialsId: 'emnabenzina', variable: 'dockerHubPwd')]) {
            bat "docker login -u emnabenzina -p ${dockerHubPwd}"
}
         bat "docker push emnabenzina/DataCamp:${DOCKER_TAG}"

}
}
      }
      }
      
def getVersion(){
    def version = bat returnStdout: true,script: 'git rev-parse --short HEAD'
    return version.trim()
}
