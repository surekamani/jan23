pipeline {
agent {
label 'docker'
}
environment {
LOGIN_CREDENTIALS=credentials('kubernete')
}
stages {
stage('checkout') {
steps {
git branch: 'main', url: 'https://github.com/surekamani/jan23.git'
}
}
stage('build docker image'){
steps {
sh 'docker build -t surekamani/jan23:$BUILD_NUMBER .'
}
}
stage('push to docker hub'){
steps {
sh 'echo $LOGIN_CREDENTIALS_PSW | docker login -u $LOGIN_CREDENTIALS_USR --password-stdin'
sh 'docker push surekamani/jan23:$BUILD_NUMBER'
}
}
stage('deploy docker image'){
steps {
sh "docker run -itd -p 80:80 -p 8080:8080 surekamani/jan23:$BUILD_NUMBER" }
}
stage('cleanup'){
steps {
cleanWs()
}
 }
 }
}

