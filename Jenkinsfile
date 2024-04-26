pipeline {
    agent any
    stages {
        stage("docker login") {
            steps {
                echo " ============== docker login =================="
                withCredentials([usernamePassword(credentialsId: 'dockerhub_id', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    script {
                        def loginResult = sh(script: "docker login -u $USERNAME -p $PASSWORD", returnStatus: true)
                        if (loginResult != 0) {
                            error "Failed to log in to Docker Hub. Exit code: ${loginResult}"
                        }
                    }
                }
            }
        }
        stage('DockerPS') {
            steps {
                echo " ============== docker APACHE =================="
                script {
                    sh 'docker pull lendy123/shoptest:latest || true' // Pull the image if exists, ignore error if not
                    sh 'docker run -d -p 8446:80 lendy123/shoptest:latest'
                }
                echo " ============== docker APACHE completed =================="
            }
        }
    }
}
