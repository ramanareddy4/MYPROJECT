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
                sh 'docker tag hello-world ramanareddy4k/dev:latest'
                }
          }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                sh 'docker login -u xxx -p xxx'
                sh 'docker push ramanareddy4k/dev:latest'
              } 
          }
        }
     }

