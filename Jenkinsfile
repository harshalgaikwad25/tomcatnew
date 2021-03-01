pipeline {
environment {
imagename = "harshalgaikwad/web"
registryCredential = 'ba7b7eb712fae907ec0639330e8075e7977fe8c3'
dockerImage = ''
}
agent any
stages {
stage('Cloning Git') {
steps {
git([url: 'https://github.com/harshalgaikwad25/tomcatnew.git', branch: 'master', credentialsId: '090df282da608bf5848004213156d4d2d04abc04'])
}
}
stage('Building image') {
steps{
script {
dockerImage = docker.build imagename
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
stage('Remove Unused docker image') {
steps{
sh "docker rmi $imagename:$BUILD_NUMBER"
sh "docker rmi $imagename:latest"
}
}
}
}
