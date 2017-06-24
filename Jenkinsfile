pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        tool(name: '3.5.0', type: 'maven')
        sh 'mvn clean install'
      }
    }
    stage('Static Code Analysis') {
      steps {
        sh 'mvn sonar:sonar'
      }
    }
    stage('Notify') {
      steps {
        emailext(subject: '$JENKINS_JOB_URL $JOB_STATUS', attachLog: true, to: 'kr@rhels.com', body: '$JENKINS_JOB_URL $JOB_STATUS')
      }
    }
  }
}