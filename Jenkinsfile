node('master') {
    stage('build'){
		dir('docker'){
			app = docker.build("rgonzalez01/apigee-cicd-base-image")
		}
    }
	stage('push'){
		docker.withRegistry('https://registry.hub.docker.com', 'rgonzalez-dockerhub') {
            app.push("latest")
        }
	}
}