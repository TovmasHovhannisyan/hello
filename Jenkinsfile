pipeline {

  agent any

  stages {

   
      stage("Build image") {
            steps {
                sh  ls > test.txt
                sh  cat test.txt
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
