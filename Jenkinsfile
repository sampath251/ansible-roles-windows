#!groovy

def err
def status = "Success"


    node {
        withCredentials([
                [
                        $class          : 'UsernamePasswordMultiBinding',
                        credentialsId   : 'AIMArtifactory',
                        passwordVariable: 'artifactory_password',
                        usernameVariable: 'artifactory_user'
                ],
                [
                        $class          : 'UsernamePasswordMultiBinding',
                        credentialsId   : 'gitlab-integration',
                        passwordVariable: 'GIT_PASSWORD',
                        usernameVariable: 'GIT_USER'
                ]
        ]) {
            
            stage('pull from SCM') {
			checkout scm
			}
        
            stage('Push ansible-batch-servers-2019.zip to artifactory') {
                sh'''
                    zip -r ansible-batch-servers-2019.zip ansible/*
                    curl -v -u ${artifactory_user}:${artifactory_password} -X PUT -T *.zip "https://artifacts.aimspecialtyhealth.com/artifactory/devops-ansible-templates/ansible-batch-servers-2019.zip"
                    
					'''
            }
        }
	}
