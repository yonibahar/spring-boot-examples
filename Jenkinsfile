pipeline {
  agent {
    node {
      label 'centos7-nodejs'
    }

  }
  stages {
    stage('Checkout code') {
      steps {
        cleanWs()
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

    stage('Increment POM') {
      steps {
        sh '''cd spring-boot-package-war/
 mvn build-helper:parse-version versions:set -DnewVersion=0.0.1.$BUILD_ID-SNAPSHOT'''
      }
    }

    stage('Package') {
      steps {
        sh '''cd spring-boot-package-war/
mvn clean package'''
      }
    }

    stage('Slack & Chuck') {
      parallel {
        stage('Notify slack') {
          steps {
            slackSend(message: 'Build Success - Module2', token: 'umVhmfifUUaxnxtOdQdSpAaN', channel: 'int-project', notifyCommitters: true)
          }
        }

        stage('Chuck norris') {
          steps {
            chuckNorris()
          }
        }

      }
    }

  }
}
