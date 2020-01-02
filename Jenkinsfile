GITHUB_PROJECT = "https://github.com/saisasank/JenkinsTest"
GITHUB_BRANCH = '${env.BRANCH_NAME}'

node("master"){
	stage('branchlist'){
		sh "echo 'Initializing workflow'"
		//checkout code
		sh "echo ${GITHUB_PROJECT}"
		git url: GITHUB_PROJECT
		sh 'git branch -r | awk \'{print $1}\' ORS=\'\\n\' > branches.txt'
		sh "cat branches.txt"
		sh "pwd"
		sh "ls -la"
		sh "cut -d '/' -f 2 branches.txt > branch.txt"
		//sh “sed s’/origin”\’///g branches.txt > branch.tx”
		//sed ‘s/$/from S0 to S1/’
	}
	stage('get build branch Parameter User Input') {
		liste = readFile 'branch.txt'
		echo "please click on the link here to chose the branch to build"
		env.BRANCH_SCOPE = input message: 'Please choose the branch to build ', ok: 'Validate!',
			parameters: [choice(name: 'BRANCH_NAME', choices: "${liste}", description: 'Branch to build?')]
	}
	stage('Checkout external proj') {
		echo "${env.BRANCH_SCOPE}"
		git branch: "${env.BRANCH_SCOPE}",
			credentialsId: 'Telcel',
			url: 'https://github.com/saisasank/JenkinsTest'
		sh “ls -lat”
	}
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
		build job: 'JenkinsDownTest', parameters: [[$class: 'StringParameterValue', name: 'COMMIT', value: "${GIT_COMMIT_HASH}"]]
	}
}}
}

