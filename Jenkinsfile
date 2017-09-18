#!/usr/bin/env groovy
pipeline {
  agent any
  tools {
    maven "M3"
  }
  stages {
    stage('Preparation') {
      steps {
        git([url: 'git@github.com:jairoandre/demo.git', branch: 'master', credentialsId: '6b440d8a-2871-426f-bf18-c2588f5fdf51'])
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
