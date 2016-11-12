timestamps {
node ('master'){
  stage 'Build'
  checkout scm
  sh './gradlew clean build'
  sh 'ls build'
  stash includes: 'build/**/*', name: 'build'
 }
 
 node ('slave'){
  stage 'Accept'
  checkout scm
  unstash 'build'
  sh 'ls build'
 }
 }