pipeline {

  agent any

      stage("Build image") {
            steps {
                script {
                    docker build -t tovmas94/hello .
                }
            }
        }
