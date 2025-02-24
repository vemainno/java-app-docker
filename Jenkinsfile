node{

def mavenHome = tool name: "maven3.9.9"
def build = BUILD_NUMBER

stage('Github code'){
git branch: 'docker', changelog: false, credentialsId: '563499a6-b9cf-47ed-abda-6f2ad570b390', poll: false, url: 'https://github.com/vemainno/java-app-docker.git'
}
stage('maven'){
sh "${mavenHome}/bin/mvn clean package"
}
stage('Docker build'){
sh "docker build -t vemana09/java-web:${build} ."
}
stage('Docker login & push'){
withCredentials([string(credentialsId: '7116d20f-7284-427a-a09b-e45f8c3cb063', variable: 'credentials')]) {
sh "docker login -u vemana09 -p ${credentials}"
}
sh "docker push vemana09/java-web:${build}"
}
stage('Deploy to AWS'){
sshagent(['562ccf02-ad83-4c05-9c40-0cedd8b45ed6']) {
sh "ssh -O StrictHostKeyChecking=no ubuntu@3.110.217.173 docker rmi -f java-web* || true "
}
}

}//node closing
