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
      sh 'echo ${DOCKER_TAG}'
        sh 'sudo docker build -t emnabenzina/testAngular:${DOCKER_TAG} .'
    }
}
      }


      }
      
def getVersion(){
    def version = sh returnStdout: true,script: 'git rev-parse --short HEAD'
    return version.trim()
}
