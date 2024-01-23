pipeline {
    agent any
        environment {
        DOCKER_IMAGE = 'web'
        CONTAINER_NAME = 'some-nginx5'
        PORT_MAPPING = '8081:80'  // Adjust the port mapping as needed
    }
    stages {
        stage('Checkout') {
            steps {
                deleteDir()
                checkout([$class: 'GitSCM', branches: [[name: 'main']], userRemoteConfigs: [[url: 'https://github.com/syerarindang/panteek.git']]])
                        // Tambahkan pernyataan log untuk menampilkan direktori saat ini
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    // Run Docker container based on the built images
                    docker.image("${DOCKER_IMAGE}").run("-p ${PORT_MAPPING} --name ${CONTAINER_NAME}")
                }
            }
        }
          stage('Run Docker Container2') {
            steps {
                script {
                    dir('panteek'){
                    docker.image("${DOCKER_IMAGE}").run("-p ${PORT_MAPPING} --name ${CONTAINER_NAME}")
                    }
                    // Run Docker container based on the built images
                }
            }
        }
          stage('Run Docker Container3') {
            steps {
                script {
                  dir('panteek'){
                    sh 'docker run --name web_server -d -p 8081:80 web'
                  }
                }
            }
        }
          stage('Run Docker Container5') {
            steps {
                script {
                    sh 'docker run --name web_server -d -p 8081:80 web'
                }
            }
        }
    }


    post {
        always {
            script {
                // Stop and remove the Docker container after execution
                docker.image("${DOCKER_IMAGE}").stop()
                docker.image("${DOCKER_IMAGE}").remove()
            }
        }
    }
}
