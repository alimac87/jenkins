node ('linux'){
  stage 'Build'
  checkout scm
  sh 'echo Build'
  sh 'echo Build >> out.txt'
 }
 
 node ('linux'){
  stage 'Accept'
  checkout scm
  sh 'echo Accept'
  sh 'echo Accept >> out.txt'
  sh 'cat out.txt'
 }