pipeline {
  agent any
  
  stages {
    stage('first') {
      steps {
        echo 'first, non-parallel stage'
      }
    }

    stage('top-parallel') {
      steps{
        echo 'top-parallel'
      }
      stages {
        stage('first-parallel') {
          steps {
            echo 'First of the parallel stages without further nesting'
            sleep 60
          }
        }
        stage('second-parallel') {
          steps{
            echo 'second-parallel'
          }
          stages {
            stage('first-nested-parallel') {
              steps {
                 echo 'the first of the nested parallel stages'
                 sleep 30
              }
           }
           stage('second-nested-parallel') {
              steps {
                 echo 'the second of the nested parallel stages'
                 sleep 30
              }
            }
          }
        }
      }
    }
  }
}
