#!groovy

pipeline {
    agent {
        docker {
            image 'maven:3.5.0-jdk-8'
        }
    }

    parameters {
        string(name: 'APP_VERSION', description: 'Demo application version')
    }
    options {
        disableConcurrentBuilds()
        buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr: '2'))
    }
    stages {
       stage('Building'){
            steps{
                echo 'mvn package'
                sh 'ls -la'
                sh 'pwd'
                sh 'which mvn'
            }
        }
        stage('Publishing artifacts'){
            steps{
                echo 'docker push'
            }
        }
        stage('Integration test'){
            steps{
                script {
                    echo 'Run image, prepare environment settings and run tests'
                }
            }
        }
    }
    post {
        changed {
            echo "CloudBees job '${JOB_NAME}' build ${BUILD_DISPLAY_NAME} status has changed to: ${currentBuild.currentResult}! Please go to ${BUILD_URL} for details."
            //mail(to: "josip.gracin@ingemark.com", subject: "CloudBees job '${JOB_NAME}' build ${BUILD_DISPLAY_NAME} status has changed to: ${currentBuild.currentResult}!", body: "Please go to ${BUILD_URL} for details.")
        }
    }
}
