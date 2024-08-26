def dockerImage;

node('docker'){
	stage('SCM'){
		checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/kubagdynia/JenkinsDocker']]])
	}
	stage('build'){
		docker.withRegistry('https://index.docker.io/v1/', 'dockerhubcreds') {
			sh 'docker buildx create --name cbbspace'
			sh 'docker buildx use cbbspace'
			sh 'docker buildx build -t devkaptain/simplednc:jenkinsfile --platform=linux/amd64,linux/arm/v7 - < dncgit.Dockerfile --push'
		}
	}
}