pipeline {
  agent {
    node {
      label 'centos7-nodejs'
    }

  }
  stages {
    stage('Check Out Code') {
      steps {
        git(url: 'https://github.com/yonibahar/spring-boot-examples.git', branch: 'yonibahar_sol', changelog: true)
      }
    }

  }
}