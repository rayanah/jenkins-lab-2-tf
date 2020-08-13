pipeline {
  agent {
    docker {
      image "bryandollery/terraform-packer-aws-alpine"
      args "-u root --entrypoint=''"
    }
  }
  environment {
    CREDS = credentials('rayanah')
        AWS_ACCESS_KEY_ID="${CREDS_USR}"
        AWS_SECRET_ACCESS_KEY="${CREDS_PSW}"
        OWNER= "rayanah"
        TF_NAMESPACE="rayanah"
        PROJECT_NAME="web-server"
         AWS_PROFILE="kh-labs"
  }
  stages {
      stage("init") {
          steps {
	      sh 'pwd'
	      sh 'terraform force-unlock 6d594d97-18d0-1ea4-e58d-c04ac16d0510'
              sh 'yes'
              sh 'make init'
              sh 'chmod -R a+rwx .terraform ssh'
              sh 'time terraform plan -out plan.out -lock=false'
           }
      }
      stage("plan") {
          steps {
              sh 'make plan'
          }
      }
      stage("apply") {
          steps {
              sh 'make apply'
              sh 'cat ip_address.txt'
          }
      }
  }
}
