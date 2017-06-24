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
  stage("SonarQube analysis") {
          node {
              withSonarQubeEnv('My SonarQube Server') {
                 sh 'mvn sonar:sonar'
              }
          }
      
  }
  stage("Quality Gate"){
          timeout(time: 1, unit: 'HOURS') {
              def qg = waitForQualityGate()
              if (qg.status != 'OK') {
                  error "Pipeline aborted due to quality gate failure: ${qg.status}"
              }
          }
      
  }
  stage('Notify') {
      steps {
        emailext(subject: '$JENKINS_JOB_URL $JOB_STATUS', attachLog: true, to: 'kr@rhels.com', body: '$JENKINS_JOB_URL $JOB_STATUS')
      }
    }
  }
}
