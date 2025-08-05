pipeline {
    agent any

    tools {
        maven 'Maven 3'     // Jenkins me Maven install hona chahiye (global tool config se)
        jdk 'Java 11'       // Jenkins me Java install hona chahiye (global tool config se)
    }

    environment {
        IMAGE_NAME = "jenkins-java-webapp"
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/saurabhgusain09/jenkins-java-webapp.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 9090:8080 $IMAGE_NAME'
            }
        }
    }
}
