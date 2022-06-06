pipeline {
    agent any
    options {
        timeout(time: 1, unit: 'HOURS')
    }
    environment {
        SOURCECODE_JENKINS_CREDENTIAL_ID = 'credentials'
        SOURCE_CODE_URL = 'https://github.com/inspirit941/todo-with-cicd.git'
        RELEASE_BRANCH = 'master'
    }
    stages {
        stage('init') {
            steps {
                echo 'clear'
                sh "ls -al"
                echo 'git branch'
            }
        }

        stage('clone') {
            steps {
                git url: SOURCE_CODE_URL, branch: RELEASE_BRANCH, credentialsId: SOURCECODE_JENKINS_CREDENTIAL_ID         
                sh "ls -al"

            }
        }

        stage('frontend dockerizing') {
            steps {
                sh "docker build -t todo/frontend ./frontend"
            }
        }

        stage('backend dockerizing') {
            steps {
                sh "pwd"
                dir("./backend"){
                    sh "pwd"

                    sh "./gradlew clean"
                    sh "./gradlew bootJar"

                    sh "docker build -t todo/backend ."
                }
            }
        }
    }
}
