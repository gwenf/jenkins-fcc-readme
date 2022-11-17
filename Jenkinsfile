pipeline {
  agent any
  stages {
    stage('Check Codes') {
      steps {
        git(url: 'https://github.com/odidia/jenkins-fcc-readme', branch: 'dev')
      }
    }

  }
}