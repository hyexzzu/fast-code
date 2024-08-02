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
        stage('start') {
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