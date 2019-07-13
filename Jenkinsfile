def registry='csudharsan/my-nginx-app'
pipeline {

   agent any 

   stages {
    stage('Docker build') {
        steps {
            script {
                sh 'docker build -t '+registry+' .'
                sh 'docker push '+registry
            }

        }
    }
  }
}
