node("master"){
	stage('Clean Workspace'){
		cleanWs()
	}
	
	stage('Code Checkout'){
		checkout([$class: 'GitSCM', branches: [[name: "master"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: "https://github.com/saisasank/JenkinsTest"]]])
	}
	
	stage('commitid'){
		sh "ls -la"
		GIT_COMMIT_HASH = sh (script: "git log -n 1 --pretty=format:'%H'", returnStdout: true)
		sh "echo ${GIT_COMMIT_HASH}"
	}
	
	stage('Triggering CD Pipeline'){
		build job: 'JenkinsDownTest', parameters: [$class: 'StringParameterValue', name: 'COMMIT', value: "${GIT_COMMIT_HASH}"]
	}
}

