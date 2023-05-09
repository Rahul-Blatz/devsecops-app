pipeline {
  agent any
  tools{
    maven 'Maven'
  }
  stages{
    stage('Initialize'){
      steps{
        sh '''
          echo "PATH = ${PATH}"
          echo "M2_HOME = ${M2_HOME}"
        '''
      }
    }
    stage ('Check-Git-Secrets') {
      steps {
        sh 'rm trufflehog || true'
        sh 'docker run gesellix/trufflehog --json https://github.com/Rahul-Blatz/devsecops-app.git > trufflehog'
        sh 'cat trufflehog'
      }
    }
    stage('Build'){
      steps{
        sh 'mvn clean package'
      }
    }
    stage('Test') {
      steps{
        echo 'Testing...'
        snykSecurity(
          snykInstallation: 'Snyk'
          snykTokenId: 'blatz-snyk-api-token'
        )
      }
    }
    stage('Deploy-to-Tomcat'){
      steps{
         sshagent(credentials: ['tomcat']) {
                sh 'scp -o StrictHostKeyChecking=no target/*.war unix@dev-sec-ops-tomcat-vm:/prod/apache-tomcat-9.0.74/webapps/webapp.war'
              }
      }
    }
  }
}
