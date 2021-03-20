podTemplate(containers: [containerTemplate(name: 'tc-ci', image: 'techcrumble/ci-image:v1.0.0', ttyEnabled: true, command: 'cat')]) {
  node(POD_LABEL) {
    stage('Run shell') {
      container('tc-ci') {
        sh "echo hello from $POD_CONTAINER" // displays 'hello from mycontainer'
        sh "env"
        sh "kubectl get pods -n jenkins"
      }
    }
    stage('checkout') {
      container('tc-ci') {
        git branch: 'main', url: 'https://github.com/ArunaLakmal/jenkins-apps.git'
        sh "ls"
        sh "kubectl apply -f ./manifests/sample-app.yaml"
      }
    }
  }
}
