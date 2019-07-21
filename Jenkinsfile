pipeline {
    agent {
        dockerfile {
            // image 'dockerhub.xxxx.com/xxxx-dev-docker/centos:7.6.1810'
            filename 'Dockerfile.infra'
            dir 'build-infra'
            args "--privileged -u root -v /var/run/docker.sock:/var/run/docker.sock"
            registryUrl 'https://hub.docker.com'
            registryCredentialsId 'hubdockercom'
        }
    }
    stages {
        stage('Preparation') {
            steps {
                script {
                    sh 'git rev-parse --short HEAD > .git/commit-id'
                    env.build_label = readFile('.git/commit-id').trim()
                    currentBuild.displayName=env.build_label                }
            }

        }
        stage('Build & Push Docker Images') {
            steps{
                echo 'Starting to build docker image'
                script{
                    def imageName = "hub.docker.com/csudharsan/${currentBuild.displayName}"
                    docker.withRegistry("https://hub.docker.com", 'hubdockercom'){
                        def customImage = docker.build(imageName, " .")
                		 customImage.push()
                        sh "docker rmi --force \$(docker images -q ${customImage.id} | uniq)"
                    }
                        
                }
            }
        }
       
    }
    post {
        always {
            deleteDir()

        }
    }
}
