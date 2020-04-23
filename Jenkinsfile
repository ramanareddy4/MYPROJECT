#!groovy
import org.jenkinsci.plugins.workflow.steps.FlowInterruptedException

def getDeploymentEnvironment() {
    if (env.BRANCH_NAME.startsWith('PR-')) {
        return 'development'
    } else if (env.BRANCH_NAME == 'master') {
        return 'production'
    }

    return env.BRANCH_NAME
}

def success_status(stage, mail_to){
    emailext ( attachLog: true,
        subject: "Dev Jenkins Job: '${env.JOB_NAME}' with Build No.: '${env.BUILD_NUMBER}' Stage: $stage has completed", 
        body: " Job: '${env.JOB_NAME}' \n Build No.: '${env.BUILD_NUMBER}' \n Build URL.: '${env.BUILD_URL}'\n Stage: $stage \n Status: Completed \n\n\n Thanks and Regards, \n One Platform Build & Release Team (Jenkins)",
        //from: mail_from,
        to: mail_to
    )
}

def failure_status(stage, mail_to){
    emailext ( attachLog: true,
        subject: "Dev Jenkins Job: '${env.JOB_NAME}' Build No.: '${env.BUILD_NUMBER}' Stage: $stage has  failed", 
        body: "Job: '${env.JOB_NAME}' \n Build No.: '${env.BUILD_NUMBER}' \n Stage: $stage \n Status: failed \n\n\n Thanks and Regards, \n One Platform Build & Release Team (Jenkins)",
        to: mail_to
    )
}

def abort_status(stage, mail_to){
    emailext ( attachLog: true,
        subject: "Dev Jenkins Job: '${env.JOB_NAME}' Build No.: '${env.BUILD_NUMBER}' Stage: $stage has  aborted", 
        body: "Job: '${env.JOB_NAME}' \n Build No.: '${env.BUILD_NUMBER}' \n Stage: $stage \n Status: aborted \n\n\n Thanks and Regards, \n One Platform Build & Release Team (Jenkins)",
        to: mail_to
    )
}

pipeline {
    agent any
     stages {
		stage('Checkout'){
            steps{
			script{
			    if(currentBuild.result == "SUCCESS"){
                  try{
					timeout(time: checkout_timeout, unit: 'SECONDS') {
					checkout scm
					success_status('Checkout', mail_to)
					}
					}catch (FlowInterruptedException timeout_error){
						currentBuild.result = 'ABORTED'
						abort_status('Checkout', mail_to)
					}
					catch(Exception err){
						currentBuild.result = 'FAILURE'
						failure_status('Checkout', mail_to)
					}
					}
				}
			}
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'docker pull hello-world'
                //docker build -t helloworld .
                sh 'docker tag hello-world ramanareddy4k/dev:test'
                }
          }
        stage('Deploy') {
            steps { 
		script{
			    if(currentBuild.result == "SUCCESS"){
                  try{
					timeout(time: checkout_timeout, unit: 'SECONDS') {
					echo 'Deploying....'
					sh 'docker login -u xxxxx -p xxxxx'
                			sh 'docker push ramanareddy4k/dev:test'
					success_status('Checkout', mail_to)
					}
					}catch (FlowInterruptedException timeout_error){
						currentBuild.result = 'ABORTED'
						abort_status('Checkout', mail_to)
					}
					catch(Exception err){
						currentBuild.result = 'FAILURE'
						failure_status('Checkout', mail_to)
					}
					}
				}
			}
        }
   }

