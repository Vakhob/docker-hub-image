pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag{}
    }
    stages{
       stage('Build Docker Image'){
           steps{
               sh "docker build . -t vakhobdevops/nodeapp:${DOCKER_TAG} "
           }
       }
       stage('Dockerhub Push'){
          steps{
              withCredentials([string(credentialsId: 'docker-hub', variable: 'dockerHubPwd')]) {
                  sh "docker login -u vakhobdevops -p ${dockerHubPwd}"
                  sh "docker push vakhobdevops/nodeapp:${DOCKER_TAG}"
              }
          }
       }
     }
}

def getDockerTag(){
    def tag = sh script: 'git rev=parse HEAD', returnStdout: true
    return tag
}
