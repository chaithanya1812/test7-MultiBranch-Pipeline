node{
def chaitu = tool name: "MAVEN"    
stage('CHECKOUT'){
    git branch: 'FIRST', url: 'https://github.com/chaithanya1812/pass.git'    
}
stage('BUILD'){
    sh "$chaitu/bin/mvn clean package"
}
stage('DEPLOY'){
    deploy adapters: [tomcat9(credentialsId: 'TOMCATIN', path: '', url: 'http://65.2.38.31:8080/')], contextPath: 'maven', war: '**/*.war'
}

}
