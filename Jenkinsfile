pipeline {
    agent any
     stages {
        stage('Build') {
            steps {
                echo 'Building..'
                checkout scm
                //docker build -t helloworld .
              }
          }
        stage('Test') {
            steps {
                scripts {
                echo 'Testing..'
                docker pull helloworld
                //docker build -t helloworld .
                // docker tag helloworld hub.docker.com/ramanareddy4k/dev:helloworld
                }
             }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
               // docker login username=ramanareddy4k@gmail.com password=Baaru143@ hub.docker.com
               // docker push hub.docker.com/ramanareddy4k/repo:helloworld
              } 
          }
        }
     }
