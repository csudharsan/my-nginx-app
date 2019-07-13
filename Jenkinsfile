def registry='csudharsan/my-nginx-app'
pipeline {

   agent any
      
   stages {
    stage('Preparation') {
        script {
            echo "prepare for build"
        }
    }
    stage('Docker build') {
        steps {
            script {
                echo 'docker build -t '+registry+' .'
                echo 'docker push '+registry
            }
        }
     }
  }
}
