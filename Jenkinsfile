pipeline {
  agent {
    node {
      label 'master'
    }
    
  }
  stages {
    stage('Sys Start') {
      parallel {
        stage('Sys Start T1') {
          steps {
            echo 'Hello World'
          }
        }
        stage('Sys Start T2') {
          steps {
            echo 'Sys Start T2'
          }
        }
        stage('Sts Start T3') {
          steps {
            echo 'Sys Start T3'
          }
        }
      }
    }
    stage('Tests') {
      parallel {
        stage('T1') {
          steps {
            echo 'T1'
          }
        }
        stage('T2') {
          steps {
            echo 'T2'
          }
        }
        stage('T3') {
          steps {
            echo 'T3'
          }
        }
      }
    }
  }
  environment {
    T1_STATUS = 'ERR'
    T2_STATUS = 'ERR'
    T3_STATUS = 'ERR'
  }
  post {
    always {
      echo 'I will always say Hello again!'
      
    }
    
  }
}