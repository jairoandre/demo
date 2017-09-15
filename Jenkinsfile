#!/usr/bin/env groovy
pipeline {
    agent any
    def mvnHome
    stage('Preparation') {
        git([url: 'git@github.com:jairoandre/demo.git', branch: 'master', credentialsId: 'b9bdf1cf-40bf-4203-8a45-949761c3c4f7'])
        mvnHome = tool 'M3'
    }
    stage('Building jars') {
        sh "'${mvnHome}/bin/mvn' clean package -Dmaven.test.skip=true"
    }
    stage('Running containers') {
        sh 'docker-compose up -d'
    }
    stage('Runnning Integration Tests') {
        sh "'${mvnHome}/bin/mvn' clean test"
    }

}
