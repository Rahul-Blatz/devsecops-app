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
    stage('Build'){
      steps{
        sh 'mvn clean package'
      }
    }
    stage('Deploy-to-Tomcat'){
      steps{
         sshagent(['tomcat']) {
                sh 'ssh -o StrictHostKeyChecking=no -l unix 35.200.196.153 uname -a'
              }
      }
    }
  }
}
