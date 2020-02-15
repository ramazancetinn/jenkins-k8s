podTemplate(containers: […]) {
  node(POD_LABEL) {
    stage('Run shell') {
      container('mycontainer') {
        sh 'echo hello world'
      }
    }
  }
}