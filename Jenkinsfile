pipeline {
  agent any
  stages {
    stage ('Checkout') {
      steps {
        git branch:'master', url: 'https://github.com/OWASP/Vulnerable-Web-Application.git'
      }
    }
    stage('Code Quality Check via SonarQube') {
      steps {
        script {
          def scannerHome = tool 'SonarQube';
            withSonarQubeEnv('SonarQube') {
            sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=. -Dsonar.host.url=http://localhost:9000 -Dsonar.login=sqp_98e3f8a858bb695f5ec9d58e4532c7499abe34d5"
            }
          }
        }
      }
    }
    post {
      always {
        recordIssues enabledForFailure: true, tool: sonarQube()
      }
    }
  }
}
