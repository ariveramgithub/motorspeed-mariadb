def network_name = "motorspeed-prod-network"
def volume_name = "motorspeed_mariadb_prod_data"
def container_name = "motorspeed-mariadb-prod"
def mariadb_root_password = "1dca#SD5.D1ad5"
def mariadb_user = "motorspeed_dba"
def mariadb_password = "1234"
def mariadb_database = "motorspeed_site"

pipeline { 
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
    // stage('Remove container...') {
    //   agent any
    //   steps {
    //     script {
    //       try {
    //         sh "docker rm -f ${container_name}"
    //         echo "Remove container ${container_name} done!"
    //       } catch(e) {
    //         echo "Container name ${container_name} not found"
    //       }
    //     }
    //   }
    // }
    stage('Docker Run') {
      agent any
      steps {
        script {
          try {
            sh "docker run -d --name ${container_name} \
            --env MARIADB_USER=${madiarb_user} \
            --env MARIADB_ROOT_PASSWORD=${mariadb_root_password} \
            --env MARIADB_PASSWORD=${mariadb_password} \
            --env MARIADB_DATABASE=${mariadb_database} \
            --network ${network_name} \
            --volume ${volume_name}:/bitnami/mariadb \
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
