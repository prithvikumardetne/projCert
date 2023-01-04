pipeline {
    agent any
    environment {
        //be sure to replace "bhavukm" with your own Docker Hub username
        DOCKER_IMAGE_NAME = "erashish01/phpwebapp"
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    app = docker.build(DOCKER_IMAGE_NAME)
                    app.inside {
                        sh 'echo Hello, World!'
                    }
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
        stage('Deploy') {
          steps {
            ansiblePlaybook credentialsId: 'ansiblekey', inventory: '/etc/ansible/hosts', playbook: 'phpplaybook.yml'
           }
        }
    }
}
