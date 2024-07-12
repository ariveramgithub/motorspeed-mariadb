pipeline {
  def network_name = "motorspeed-prod-network"
  def volume_name = "motorspeed_mariadb_prod_data"
  def container_name = "motorspeed-mariadb-prod"

  
  agent none
  stages {
    stage("Network create...") {
      agent any
      steps {
        script {
          try {
            sh "docker network create ${network_name}"
            echo "Network ${network_name} done!"
          } catch(e){
            echo "Network ${network_name} already exists"
          }
        }
      }
    }
    stage("Volume create...") {
      agent any
      steps {
        script {
          try {
            sh "docker volume create --name ${volume_name}"
            echo "Volume ${volume_name} done!"
          } catch(e){
            echo "Volume ${volume_name} already exists"
          }
        }
      }
    }
    stage('Docker Run') {
      agent any
      steps {
        script {
          try {
            sh "docker run -d --name ${container_name} \
            --env MARIADB_USER=motorspeed_dba \
            --env MARIADB_ROOT_PASSWORD=1dca#SD5.D1ad5 \
            --env MARIADB_PASSWORD=1234 \
            --env MARIADB_DATABASE=motorspeed_site \
            --network motorspeed-network \
            --volume motorspeed_mariadb_data:/bitnami/mariadb \
            -p 9036:3306 \
            --restart unless-stopped \
            bitnami/mariadb:latest"

            echo "Container ${container_name} done!"
          } catch(e){
            echo "Container ${container_name} already exists"
          }
        }
      }
    }
  }
}
