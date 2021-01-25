pipeline {
    agent {
      label {
            label "windows"
      }
    }
    options {
        disableConcurrentBuilds()
  }
  parameters {
      booleanParam(
      name: 'it',
      defaultValue: false,
      description: 'Whether to run integration tests.' )
  }
  stages {
    stage('Build') {
        steps {
            dir('HelloWorld') {
                bat 'dotnet build'
            }
        }
    }
  }
  post {
    failure {
      script {
        COMMITER_EMAIL = bat(returnStdout: true, script: 'git log -1 --pretty=format:%ae')
      }
      emailext body: '${JELLY_SCRIPT,template="bl"}', subject: "${JOB_NAME} build ${BUILD_NUMBER} ${currentBuild.currentResult}", to: "${COMMITER_EMAIL}"
    }
  }
}
