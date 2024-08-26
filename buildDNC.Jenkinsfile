def dockerImage;

node('docker'){
	stage('SCM'){
		checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/kubagdynia/JenkinsDocker']]])
	}
	stage('build'){
		dockerImage = docker.build('devkaptain/agent-dnc:v' + env.BUILD_NUMBER, './dotnetcore');
	}
	stage('push'){
		docker.withRegistry('', 'dockerhubcreds') {
			dockerImage.push();
		}
	}
}