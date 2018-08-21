podTemplate(label: 'docker', yaml: """
apiVersion: v1
kind: Pod
metadata:
  labels:
    some-label: some-label-value
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
    container('docker'){
    checkout scm
    echo "LEL! ${env}"
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
}