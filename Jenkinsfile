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

      }
      }
def getVersion(){
    def version = sh returnStdout: true,script: 'git rev-parse --short HEAD'
    return version.trim()
}
