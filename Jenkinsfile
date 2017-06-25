def mvnHome
stage('Preparation') { 
    node {
        git 'https://github.com/vbottu/java-getting-started.git'
    }
}

stage("build & SonarQube analysis") {
  node {
    mvnHome = tool '3.5.0'
     withSonarQubeEnv('Local') {
       sh "${mvnHome}/bin/mvn clean package sonar:sonar"
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
