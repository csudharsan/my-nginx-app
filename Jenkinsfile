def registry='csudharsan/my-nginx-app'
pipeline {

    stage('Docker build') {
        steps {
            script {
                sh 'docker build -t '+registry+' .'
                sh 'docker push '+registry
            }

        }

    }
}
