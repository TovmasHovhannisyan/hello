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
 
  }

}
