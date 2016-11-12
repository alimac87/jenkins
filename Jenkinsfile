node ('linux'){
  stage 'Build'
  checkout scm
  sh 'echo Build > abc.txt'
 }
 
 node ('linux'){
  stage 'Accept'
  checkout scm
  sh 'echo Accept'
  sh 'cat abc.txt'
 }