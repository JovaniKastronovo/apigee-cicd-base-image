podTemplate(label: 'docker', yaml: """
apiVersion: v1
kind: Pod
metadata:
  labels:
    some-label: docker
spec:
  containers:
  - name: docker
    image: docker
    command:
    - cat
    tty: true
    env:
    - name: POD_IP
	  valueFrom: 
	    fieldRef:
		  fieldPath: status.hostIP
"""
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