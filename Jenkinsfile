GITHUB_PROJECT = "https://github.com/saisasank/JenkinsTest"
GITHUB_BRANCH = '${env.BRANCH_NAME}'

node("master"){
	stage('List Branch'){
		sh "echo 'Initializing workflow'"
		//checkout code
		sh "echo ${GITHUB_PROJECT}"
		git url: GITHUB_PROJECT
		sh 'git branch -r | awk \'{print $1}\' ORS=\'\\n\' > branches.txt'
		sh "cat branches.txt"
		sh "pwd"
		sh "ls -la"
		sh "cut -d '/' -f 2 branches.txt > branch.txt"
	}
	stage('Branch Parameter Input') {
		liste = readFile 'branch.txt'
		echo "please click on the link here to chose the branch to build"
		env.BRANCH_SCOPE = input message: 'Please choose the branch to build ', ok: 'Validate!', parameters: [choice(name: 'BRANCH_NAME', choices: "${liste}", description: 'Branch to build?')]
	}
	stage('Clean Workspace'){
		cleanWs()
	}
	stage('Code Checkout'){
		echo "${env.BRANCH_SCOPE}"
		checkout([$class: 'GitSCM', branches: [[name: "${env.BRANCH_SCOPE}"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: "https://github.com/saisasank/JenkinsTest"]]])
	}
	stage('commitid'){
		sh "ls -la"
		GIT_COMMIT_HASH = sh (script: "git log -n 1 --pretty=format:'%H'", returnStdout: true)
		sh "echo ${GIT_COMMIT_HASH}"
	}
	stage('Triggering CD Pipeline'){
		build job: 'JenkinsDownTest', parameters: [[$class: 'StringParameterValue', name: 'COMMIT', value: "${GIT_COMMIT_HASH}"]]
	}
}

