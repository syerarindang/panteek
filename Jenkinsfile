pipeline {
    agent any
        environment {
        DOCKER_IMAGE = 'web'
        CONTAINER_NAME = 'some-nginx5'
        PORT_MAPPING = '8081:80'  // Adjust the port mapping as needed
    }
    stages {
        // stage('Checkout') {
        //     steps {
        //         deleteDir()
        //         checkout([$class: 'GitSCM', branches: [[name: 'main']], userRemoteConfigs: [[url: 'https://github.com/syerarindang/panteek.git']]])
        //                 // Tambahkan pernyataan log untuk menampilkan direktori saat ini
        //     }
        // }
        stage('Run Docker Container') {
            steps {
                script {
                    // Run Docker container based on the built images
                    docker.image("${DOCKER_IMAGE}").run("-p ${PORT_MAPPING} --name ${CONTAINER_NAME}")
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
