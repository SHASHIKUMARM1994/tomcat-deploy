pipeline {
 agent any
 environment {
 IMAGE_NAME = 'tomcat-sample-app'
 CONTAINER_NAME = 'tomcat-app'
 PORT_MAPPING = '9191:8080' // Host:Container
 }
 stages {
 stage('Checkout') {
 steps {
 checkout scm
 }
 }
stage('Build Docker Image') {
 steps {
script {
 docker.build("${IMAGE_NAME}")
 }
 }
 }
 stage('Run Docker Container') {
 steps {
 script {
 sh "docker rm -f ${CONTAINER_NAME} || true"
 sh "fuser -k 9191/tcp || true"
 sh "docker run -d -p ${PORT_MAPPING} --name ${CONTAINER_NAME}
${IMAGE_NAME}"
 sh "docker ps | grep ${CONTAINER_NAME}"
 }
 }
 }
 }
}
