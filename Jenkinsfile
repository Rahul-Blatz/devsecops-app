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
          sh '''
            cd ~
            sudo cd .ssh
            sudo ssh -i jenkins-keys unix@dev-sec-ops-tomcat-vm
            Fisher@12
            echo $USER
            '''
      }
    }
  }
}
