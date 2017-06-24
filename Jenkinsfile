pipeline {
  agent any
  tools {
        maven '3.5.0' 
    }
  stages {
    stage('Build') {
      steps {
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
