pipeline {
  agent {
    node {
      label 'master'
    }
    
   environment {
    T1_STATUS = 'ERR'
    T2_STATUS = 'ERR'
    T3_STATUS = 'ERR'
  }
    
  }
  stages {
    stage('Sys Start') {
      parallel {
        stage('Sys Start T1') {
          steps {
            echo 'Hello World'
            sleep 30
            T1_STATUS = 'SUCCESS'
          }
        }
        stage('Sys Start T2') {
          steps {
            echo 'Sys Start T2'
            sleep 10
            T2_STATUS = 'SUCCESS'
          }
        }
        stage('Sts Start T3') {
          steps {
            echo 'Sys Start T3'
            sleep 50
            T3_STATUS = 'SUCCESS'
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
  post {
    always {
      echo 'I will always say Hello again!'
      
    }
    
  }
}
