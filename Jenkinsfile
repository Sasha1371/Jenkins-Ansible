pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dckr_pat_ZccV2yLN5weYNwRJhLTS2LXI5hg')
    }
    stages {
        stage("docker login") {
            steps {
                echo " ============== docker login =================="
                script {
                    withCredentials([usernamePassword(credentialsId: DOCKERHUB_CREDENTIALS, usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
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
                echo " ============== docker install apache =================="
                sh 'docker build -t lendy123/shoptest:latest1 .'
                sh 'docker run -d -p 8446:80 lendy123/shoptest:latest1'
                sh 'docker push lendy123/shoptest:latest'
                echo " ============== docker completed =================="
            }
        }
    }
}
