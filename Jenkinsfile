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
mvn compile'''
      }
    }

    stage('Test mvn') {
      steps {
        sh '''cd spring-boot-package-war/
mvn test'''
      }
    }

    stage('Package') {
      steps {
        sh '''cd spring-boot-package-war/
mvn clean package'''
      }
    }

    stage('Notify Slack') {
      steps {
        slackSend(token: 'umVhmfifUUaxnxtOdQdSpAaN', channel: ' int-project', notifyCommitters: true, message: 'Build Success')
      }
    }

  }
}