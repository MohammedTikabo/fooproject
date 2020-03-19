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
          }

             stage('Create coverage report') {
                      steps {
                           sh "mvn cobertura:cobertura"
                      }
                }
            stage('newman') {
             steps {
                 sh 'newman run "Restful Booker.postman_collection.json" --environment "Restful Booker.postman_environment.json" --reporters junit'
             }
             post {
                 always {
                         junit '**/*xml'
                     }
                 }
         }
         stage('robot') {
                     steps {
                             sh 'robot -d results --variable BROWSER:headlesschrome Carboking.robot'
                     }
                     post {
                         always {
                             script {
                                   step(
                                         [
                                           $class              : 'RobotPublisher',
                                           outputPath          : 'results',
                                           outputFileName      : '**/output.xml',
                                           reportFileName      : '**/report.html',
                                           logFileName         : '**/log.html',
                                           disableArchiveOutput: false,
                                           passThreshold       : 50,
                                           unstableThreshold   : 40,
                                           otherFiles          : "**/*.png,**/*.jpg",
                                         ]
                                    )
                             }
                         }
                     }
                 }

    }
    post {
                  always {
                     
                     junit '**/*xml'
                                     step([$class: 'CoberturaPublisher', autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: '**/coverage.xml', failUnhealthy: false, failUnstable: false, maxNumberOfBuilds: 0, onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false])

                             }
                         }
                     }






