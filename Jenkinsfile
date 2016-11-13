@Library('https://gitlab.com/alimac87/fabric8-pipeline-library/raw/master')

def apiUrl = new URL("https://raw.githubusercontent.com/alimac87/jenkins/master/abc.json")
def rs = restGetURL{
  url = apiUrl
  authString = ""
}

println rs

def BUILD_VERSION = "1.0.${currentBuild.number}"

timestamps {
  node ('master'){
    stage 'Build'
    checkout scm
    sh './gradlew clean build'
    sh 'ls build'
    stash includes: 'build/**/*', name: 'build'
    try {
      withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'alimac87.github', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD']]) {
        sh("git config credential.username ${env.GIT_USERNAME}")
        sh("git config credential.helper '!echo password=\$GIT_PASSWORD; echo'")
        sh("git config user.email \"${env.GIT_USERNAME}@example.com\"")
        sh("git config user.name \"${env.GIT_USERNAME}\"")
        sh("git tag -a ${BUILD_VERSION} -m 'Create tag'")
        sh("GIT_ASKPASS=true git push origin --tags")
      }
    } finally {
      sh("git config --unset credential.username")
      sh("git config --unset credential.helper")
    }
  }

  node ('slave'){
    stage 'Accept'
    checkout scm
    unstash 'build'
    sh 'ls build'
  }
}