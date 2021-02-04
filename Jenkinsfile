pipeline {
  agent {
    kubernetes {
      defaultContainer 'dind'
      yamlFile 'KubernetesPod.yaml'
    }
  }


  stages {

      stage("Build image") {
            steps {
                script {
                    myapp = docker.build("tovmas94/hello:${env.BUILD_ID}")
                }
            }
        }   
    
      stage("Push image") {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                            myapp.push("latest")
                            myapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }
    
      stage('Deploy App') {
        steps {
          script {
            sh 'wget https://dl.k8s.io/release/v1.19.3/bin/linux/amd64/kubectl -P /usr/local/bin/ && chmod 770 /usr/local/bin/kubectl && wget https://github.com/digitalocean/doctl/releases/download/v1.54.0/doctl-1.54.0-linux-amd64.tar.gz && tar xf doctl-1.54.0-linux-amd64.tar.gz && mv doctl /usr/local/bin'
            kubernetesDeploy(configs: "hellowhale.yml", kubeconfigId: "k8s-popupschool")
          }
        }
      }    
    
  }

}
