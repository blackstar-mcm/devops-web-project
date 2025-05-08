pipeline {
    agent {
        node {
            label 'dockerhost-build-server'
        }
    }
    tools {
        maven 'maven-3.9.6'
    }
    stages {
        stage('Packaging') {
            steps {
                echo 'Packaging..'
                sh 'mvn clean package'
            }
        }
        stage('Copying war file') {
            steps {
                echo 'Copying war file..'
                sh 'mv target/*.war .'
            }
        }
        stage('build image') {
            steps {
                sh 'docker build -t miichellecanete/devops-web-project:v1 --label devops-web-project-server .'
            }
        }
        stage('run container') {
            steps {
                sh 'docker run -d --name devops-web-project-server --label devops-web-project-server -p 8081:8080 miichellecanete/devops-web-project:v1'
            }
        }
    }
}
