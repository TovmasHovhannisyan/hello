pipeline {

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/TovmasHovhannisyan/hellowhale.git', branch:'master'
      }
    }
    
      stage("Build image") {
            steps {
                script {                   
                    myapp = docker.build("tovmas94/hellowhale:${env.BUILD_ID}")
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
        


stage("Deploy to Staging"){
            when {
                branch 'tovmas/hellowhale-1'
            }
            steps {
                kubernetesDeploy kubeconfigId: 'k8s-cluster', configs: 'hellowhale-stg.yml', enableConfigSubstitution: true  // REPLACE kubeconfigId
             }
            post{
                success{
                    echo "Successfully deployed to Staging"
                }
                failure{
                    echo "Failed deploying to Staging"
                }
            }
        }
        

    
stage("Deploy to Production"){
            when {
                branch 'master'
            }
            steps { 
                kubernetesDeploy kubeconfigId: 'k8s-cluster', configs: 'hellowhale-prod.yml', enableConfigSubstitution: true  // REPLACE kubeconfigId
 
             }
            post{
                success{
                    echo "Successfully deployed to Production"
                }
                failure{
                    echo "Failed deploying to Production"
                }
            }
        }
        
                   


}
