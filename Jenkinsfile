pipeline {
  agent {
    node {
      label 'centos7-nodejs'
    }

  }
  stages {
    stage('Checkout code') {
      steps {
        git(url: 'https://github.com/yonibahar/spring-boot-examples.git', branch: 'yonibahar_sol', changelog: true)
      }
    }

    stage('Compile maven') {
      steps {
        sh '''cd spring-boot-package-war/
mvn compile'''
      }
    }

    stage('Test maven') {
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
      parallel {
        stage('Notify slack') {
          steps {
            slackSend(message: 'Build Success - Module2', token: 'umVhmfifUUaxnxtOdQdSpAaN', channel: 'int-project', notifyCommitters: true)
          }
        }

        stage('Chuck Norris') {
          steps {
            chuckNorris()
          }
        }

      }
    }

    stage('Delete workspace') {
      steps {
        cleanWs(cleanWhenAborted: true, cleanWhenFailure: true, cleanWhenNotBuilt: true, cleanWhenSuccess: true)
      }
    }

  }
}