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
}//node closing
