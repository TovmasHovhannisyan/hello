pipeline {

  agent any

  stages {

   
      stage("Build image") {
            steps {
                script {
                  pwd
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
