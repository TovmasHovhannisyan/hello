pipeline {

  agent any

      stage("Build image") {
            steps {
                script {
                    sh  'docker build -t tovmas94/hello .'
                }
            }
        }
