def



timestamps {
node ('master'){
  stage 'Build'
  checkout scm
  sh './gradlew clean build'
  sh 'ls build'
  stash includes: 'build/**/*', name: 'build'
  try {
  withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'alimac87.gitlab', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD']]) {
    sh("git config credential.username ${env.GIT_USERNAME}")
    sh("git config credential.helper '!echo password=\$GIT_PASSWORD; echo'")
    sh("git tag -a some_tag -m 'Jenkins'")
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