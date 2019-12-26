node("master"){
	stage('Clean Workspace'){
		cleanWs()
	}
	
	stage('commitid'){
        sh "ls -la"
	sh "echo %GIT_COMMIT%"
	}
	
	stage('Triggering CD Pipeline'){
		build job: 'JenkinsDownTest', parameters: [[$class: 'StringParameterValue', name: 'COMMIT', value: "${GIT_REPO_NAME}"], [$class: 'StringParameterValue', name: 'ARTIFACT_NAME', value: "${DOCKER_IMAGE_NAME}"], [$class: 'StringParameterValue', name: 'ARTIFACT_VERSION', value: "${BUILD_VERSION}.${BUILD_NUMBER}"]]
	}
}

