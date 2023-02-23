pipeline {
   agent {label 'jenkins'}

   environment {
      DOCKERHUB_CREDENTIALS = credentials('docker')
   }

   stages {
      
      stage('Build Image'){
         steps {
            sh 'docker build -t ahmedmosaad/project .'
         }
      }

      stage('Login') {
         steps {
            sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
         }
      }

      stage('Push Image'){
         steps {
            sh 'docker push ahmedmosaad/project'
         }
      }

      stage('deploy') {
         steps {
         
               withCredentials([file(credentialsId: 'cluster-config', variable: 'config')]) {
               sh """
                     kubectl apply -f deployment --kubeconfig=${config}
                  """
            }
         }
      }
   }
}
