#!groovy

pipeline {
  agent none

stage(build)
     { 
     steps {     
       checkout scm
       docker build -t helloworld 
      }
  }  
  stage(publish to docker)
     {
      steps {
      docker tag helloworld hub.docker.com/ramanareddy4k/repo:hellowworld
      docker login username:ramanareddy4k@gmail.com password:Baaru143@ hub.docker.com
      docker push hub.docker.com/ramanareddy4k/repo:hellowworld
      }
    }
}  
  
