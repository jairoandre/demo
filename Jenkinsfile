#!/usr/bin/env groovy
pipeline {
  agent any
  tools {
    maven "M3"
    docker "docker"
  }
  stages {
    stage('Preparation') {
      steps {
        git([url: 'git@github.com:jairoandre/demo.git', branch: 'master', credentialsId: 'b9bdf1cf-40bf-4203-8a45-949761c3c4f7'])
        // Install docker compose if needed
        sh "curl -L https://github.com/docker/compose/releases/download/1.16.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose"
      }
    }
    stage('Building jars') {
      steps {
        sh "mvn clean package -Dmaven.test.skip=true"
      }
    }
    stage('Running containers') {
      steps {
        sh 'docker-compose up -d'
      }
    }
    stage('Runnning Integration Tests') {
      steps {
        sh "mvn clean test"
      }
    }
  }
}
