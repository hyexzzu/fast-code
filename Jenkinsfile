pipeline {
    agent any
    environment {
        GITNAME = 'hyexzzu'
        GITMAIL = 'bonterouge@gmail.com'
        GITWEBADD = 'https://github.com/hyexzzu/fast-code.git'
        GITSSHADD = 'git@github.com:hyexzzu/fast-code.git'
        GITCREDENTIAL = 'git_cre'
        DOCKERHUB = 'creamday/fast'
        DOCKERHUBCREDENTIAL = 'docker_cre'
    }
    stages {
        stage('Checkout Github') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [],
                userRemoteConfigs: [[credentialsId: GITCREDENTIAL, url: GITWEBADD]]])
            }
            post {
                failure {
                    sh "echo clone failed"
                }
                success {
                    sh "echo clone success"
                }
            }
        }
        stage('start2') {
            steps {
                sh "echo hello jenkins!!!"
            }
            post {
                failure {
                    sh "echo failed"
                }
                success {
                    sh "echo success"
                }
            }
        }
        stage('start3') {
            steps {
                sh "echo hello jenkins!!!"
            }
            post {
                failure {
                    sh "echo failed"
                }
                success {
                    sh "echo success"
                }
            }
        }
    }
}
}