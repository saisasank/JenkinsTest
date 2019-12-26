node("master"){
	stage('Clean Workspace'){
		cleanWs()
	}
	
	stage('commitid'){
        sh "ls -la"
	GIT_COMMIT_HASH = sh (script: "git log -n 1 --pretty=format:'%H'", returnStdout: true)
	sh "echo ${GIT_COMMIT_HASH}"
	}
	
	stage('Triggering CD Pipeline'){
		build job: 'JenkinsDownTest', parameters: [[$class: 'StringParameterValue', name: 'COMMIT', value: "${GIT_REPO_NAME}"], [$class: 'StringParameterValue', name: 'ARTIFACT_NAME', value: "${DOCKER_IMAGE_NAME}"], [$class: 'StringParameterValue', name: 'ARTIFACT_VERSION', value: "${BUILD_VERSION}.${BUILD_NUMBER}"]]
	}
}

