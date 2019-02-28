pipeline {
  agent {
    node {
      label 'ibmi'
    }
  }
  stages {
    stage('configure') {
      environment {
        OBJECT_MODE = '64'
        CC = 'gcc'
        CXX = 'g++'
      }
      steps {
        sh './config no-idea no-rc5 no-hw no-egd no-engine enable-tls1_3 shared threads -DOPENSSL_NO_SECURE_MEMORY'
        sh 'perl configdata.pm --dump'
      }
    }
    stage('build') {
      steps {
        sh 'make -j4'
      }
    }
    stage('test') {
      steps {
        sh 'make test'
      }
    }
  }
}
