node("master"){
	stage('Clean Workspace'){
		cleanWs()
	}
	
	stage('Code Checkout'){
        checkout([$class: 'GitSCM', branches: [[name: "${BRANCH}"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: "${GIT_SOURCE_CRED_ID}", url: "${GIT_SOURCE_URL}"]]])
    }
}
