podTemplate(yaml: """
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: docker
    env:
    - name: DOCKER_HOST
      value: 127.0.0.1
    image: docker:18.09
    command:
    - cat
    tty: true
  - name: tools
    image: argoproj/argo-cd-ci-builder:v0.13.1
    command:
    - cat
    tty: true
"""
  ) {

  node{
    stage('BUILD') {
        environment {
        DOCKERHUB_CREDS = credentials('dockerhub')
      }
      git 'https://github.com/jenkinsci/kubernetes-plugin.git'
      container('docker') {
          // Build new image
          sh "until docker ps; do sleep 3; done && docker build -t ramazancetin/argocd-demo:${env.GIT_COMMIT} ."
          // Publish new image
          sh "docker login --username $DOCKERHUB_CREDS_USR --password $DOCKERHUB_CREDS_PSW && docker push alexmt/argocd-demo:${env.GIT_COMMIT}"
        }
    }

  }
}