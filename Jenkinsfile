pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'     // Jenkins > Global Tool Configuration mein yeh Maven version define hona chahiye
        jdk 'JAVA_HOME'        // Same for Java
    }

    environment {
        IMAGE_NAME = "java-webapp"
        CONTAINER_NAME = "java-app-container"
        APP_PORT = "9090"
    }

    stages {

        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/saurabhgusain09/jenkins-java-webapp.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                sh 'echo "Running unit tests..."'
                // Put actual test commands here if needed
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                docker rm -f $CONTAINER_NAME || true
                docker run -d --name $CONTAINER_NAME -p $APP_PORT:8080 $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Build and Deployment Successful!"
        }
        failure {
            echo "❌ Pipeline Failed. Check logs above."
        }
    }
}

