pipeline {
  agent {
    node {
      label 'centos7-nodejs'
    }

  }
  stages {
    stage('Checkout Code') {
      steps {
        git(url: 'https://github.com/yonibahar/spring-boot-examples.git', branch: 'yonibahar_sol', changelog: true)
      }
    }

    stage('Maven Compile') {
      steps {
        sh '''cd spring-boot-package-war/
mvn build'''
      }
    }

  }
}