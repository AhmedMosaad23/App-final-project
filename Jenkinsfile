pipeline {
   agent {label 'jenkins'}

   environment {
      DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')
   }

   stages {
      
      stage('Build Image'){
         steps {
            sh 'docker build -t amrelzahar/node-application .'
         }
      }

      stage('Login') {
         steps {
            sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
         }
      }
