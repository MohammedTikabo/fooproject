pipeline {
 agent any
 stages {
 stage('Checkout') {
 steps {
 git 'https://github.com/MohammedTikabo/fooproject.git'
 }
 }
 stage('Build') {
 steps {
 bat "mvn compile"
 }
 }
 stage('Test') {
 steps {
 sh "mvn test"
 }
 post {
 always {
 junit '**/TEST*.xml'
 }
 }
 }
 }
}