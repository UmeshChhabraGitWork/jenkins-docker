pipeline {
 environment {
 imagename = "umeshhubdocker/jenkins-docker" 
 registryCredential = 'umeshhubdocker-docckerhub'
 dockerImage = ''
 }
 agent any
 stages {
 stage('Cloning Git') {
 steps {
 git([url: 'https://github.com/UmeshChhabraGitWork/jenkins-docker.git', branch: 'main'])
 }
 }
 stage('Building image') {
 steps{
 script {
 dockerImage = docker.build imagename
 }
 }
 }
 stage('Running image') {
 steps{
 script {
 sh "docker run ${imagename}:latest"
 }
 }
 }
 stage('Deploy Image') {
 steps{
 script {
 docker.withRegistry( '', registryCredential ) {
 dockerImage.push("$BUILD_NUMBER")
 dockerImage.push('latest')
 }
 }
 }
 }	
 }
}
