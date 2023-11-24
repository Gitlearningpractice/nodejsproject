pipeline {
    agent any

    triggers {
        pollSCM('H/5 * * * *') // SCM polling every 5 minutes
    }

    environment {
        DOCKER_IMAGE = 'nodejs_app'
        CONTAINER_NAME = 'nodejs_container'
        PORT_MAPPING = '8080:80'
    }
    
    stages {
        stage('Checkout') {
            steps {
                script {
                    //'https://github.com/Gitlearningpractice/nodejsproject.git'
                    // Check out your source code from version control (e.g., Git)
                    checkout scm
                
                }
            }
        
        }
        stage('Building Docker Image') {
            steps {
                script {
                   // Build the Docker image
                    docker.build("${DOCKER_IMAGE}:${BUILD_NUMBER}", '.')
                }
            }
        }

        stage('Deploying Docker Image') {
            steps {
                script {
                    // Deploy the container
                    docker.image("${DOCKER_IMAGE}:${BUILD_NUMBER}").withRun("--name ${CONTAINER_NAME} -p ${PORT_MAPPING}")
                    
                }
            }
        }
    }

}
