#!/usr/bin/env groovy
pipeline {
  agent any
  stages {
    stage('Preparation') {
      steps {
        git([url: 'git@github.com:jairoandre/demo.git', branch: 'master', credentialsId: 'b9bdf1cf-40bf-4203-8a45-949761c3c4f7'])
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
