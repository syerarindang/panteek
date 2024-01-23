pipeline {
    agent any
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
