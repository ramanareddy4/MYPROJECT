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
                echo 'Testing..'
                sh 'docker pull hello-world'
                //docker build -t helloworld .
                sh 'docker tag hello-world hub.docker.com/ramanareddy4k/dev:hello-world'
                }
          }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                sh 'docker login username=ramanareddy4k@gmail.com password=Baaru143@ hub.docker.com'
                sh 'docker push hub.docker.com/ramanareddy4k/dev:hello-world'
              } 
          }
        }
     }
