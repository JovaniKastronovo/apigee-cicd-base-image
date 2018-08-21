podTemplate(label: 'docker',
  containers: [containerTemplate(name: 'docker', image: 'docker', ttyEnabled: true, command: 'cat', envVars: [
    containerEnvVar(key: 'POD_IP', value: '''
valueFrom:
  fieldRef:
    fieldPath: status.hostIP''')
  ])]
  ) {
node('docker'){
	checkout scm
	echo sh(returnStdout: true, script: 'env')
	withDockerServer([uri: "tcp://${env.POD_IP}"]) {
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
}
}