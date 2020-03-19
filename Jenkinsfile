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
 sh "mvn compile"
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
 stage('newman') {
             steps {
                 sh 'newman run RestfulBooker.postman_collection.json --environment RestfulBooker.postman_environment.json --reporters junit'
             }
             post {
                 always {
                         junit '**/*xml'
                     }
                 }
         }
         }
 }
}