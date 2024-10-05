pipeline {
    agent any
    tools {
        maven 'my-maven'
        jdk 'my jdk'
    }
    stages {
        stage('Clone') {
            steps {
                git url: 'https://github.com/AchuthRKumar/department-service.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                bat "mvn clean install -DskipTests"
            }
        }
        stage('Test') {
            steps {
                bat "mvn test"
            }
        }
        stage('Deploy') {
            steps {
                bat "docker rm -f department-container"
                bat "docker rmi -f department-container"
                bat "docker build -t department-image ."
                bat "docker run -p 8088:8088 -d --name department-container department-image"
            }
        }
    }
}
