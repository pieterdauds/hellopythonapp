node{
  stage('build & deploy') {
    openshiftBuild bldCfg: 'hellopythonapp',
    namespace: 'i3development',
      showBuildLogs: 'true'
    openshiftVerifyDeployment depCfg: 'hellopythonapp',
      namespace: 'i3development'
  }

  stage('approval (test)') {
    input message: 'Approve for testing?',
      id: 'approval'
  }

  stage('deploy to test') {
    openshiftTag srcStream: 'hellopythonapp',
      namespace: 'i3development',
      srcTag: 'latest',
      destinationNamespace: 'i3testing',
      destStream: 'hellopythonapp',
      destTag: 'test'
    openshiftVerifyDeployment depCfg: 'hellopythonapp',
      namespace: 'i3testing'
  }

  stage('approval (i3production)') {
    input message: 'Approve for production?',
      id: 'approval'
  }

  stage('deploy to production') {
    openshiftTag srcStream: 'hellopythonapp',
      namespace: 'i3development',
      srcTag: 'latest',
      destinationNamespace: 'i3production',
      destStream: 'hellopythonapp',
      destTag: 'prod'
    openshiftVerifyDeployment depCfg: 'hellopythonapp',
      namespace: 'i3production'
  }
}
