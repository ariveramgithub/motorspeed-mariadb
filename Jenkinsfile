pipeline {
  agent none

  stages {
    /*
    stage("Network create...") {
      agent any
      steps {
        script {
          try {
            sh "docker network create motorspeed-prod-network"
            echo "Network motorspeed-prod-network done!"
          } catch(e){
            echo "Network motorspeed-prod-network already exists"
          }
        }
      }
    }
    stage("Volume create...") {
      agent any
      steps {
        script {
          try {
            sh "docker volume create --name motorspeed_mariadb_prod_data"
            echo "Volume motorspeed_mariadb_prod_data done!"
          } catch(e){
            echo "Volume motorspeed_mariadb_prod_data already exists"
          }
        }
      }
    }
    */
    stage('Docker Run') {
      agent {
        docker {
          image 'bitnami/mariadb:latest'
        }
      }
      steps {
        sh 'mariadb --version'
      }
    }
  }
}
