pipeline {
    agent any
    environment {
        GITNAME = 'hyexzzu'
        GITEMAIL = 'bonterouge@gmail.com'
        GITWEBADD = 'https://github.com/hyexzzu/fast-code.git'
        GITSSHADD = 'git@github.com:hyexzzu/deployment.git'
        GITCREDENTIAL = 'git_cre'
        DOCKERHUB = 'creamday/fast'
        DOCKERHUBCREDENTIAL = 'docker_cre'
    }
    stages {
        stage('Checkout Github') {
            steps {
                // 기본적으로 설치되는 깃허브 플러그인 신택스
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
        stage('docker image build') {
            steps {
                sh "docker build -t ${DOCKERHUB}:${currentBuild.number} ."
                sh "docker build -t ${DOCKERHUB}:latest ."
                // currentBuild.number 젠킨스가 제공하는 빌드 넘버 변수
                // creamday/fast:<빌드넘버> 와 같은 이미지 만들어질 예정
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
        stage('docker image push') {
            steps {
                withDockerRegistry(credentialsId: DOCKERHUBCREDENTIAL, url: '') {
                    sh "docker push ${DOCKERHUB}:${currentBuild.number}"
                    sh "docker push ${DOCKERHUB}:latest"
                }
            }
            post {
                failure {
                    sh "docker image rm -f ${DOCKERHUB}:${currentBuild.number}"
                    sh "docker image rm -f ${DOCKERHUB}:latest"
                    sh "ehco push failed"
                    // 성공하든 실패하든 로컬에 있는 도커 이미지는 삭제
                }
                success {
                    sh "docker image rm -f ${DOCKERHUB}:${currentBuild.number}"
                    sh "docker image rm -f ${DOCKERHUB}:latest"
                    sh "ehco push failed"
                    // 성공하든 실패하든 로컬에 있는 도커 이미지는 삭제
                }
            }
        }
        stage('EKS Manifest File Update') {
            steps {
                git credentialsId: GITCREDENTIAL, url: GITSSHADD, branch: 'main'
                sh "git config --global user.email ${GITEMAIL}"
                sh "git config --global user.name ${GITNAME}"
                sh "sed -i 's@${DOCKERHUB}:.*@${DOCKERHUB}:${currentBuild.number}@g' fast.yml"

                sh "git add ."
                sh "git branch -M main"
                sh "git commit -m 'fixed tag ${currentBuild.number}'"
                sh "git remote remove origin"
                sh "git remote add origin ${GITSSHADD}"
            }
            post {
                failure {
                    sh "echo manifest update failed"
                }
                success {
                    sh "echo clone success"
                }
            }
        }
    }
}
