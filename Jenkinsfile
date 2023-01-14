node{
def chaitu = tool name: "MAVEN"    
    
echo "The node name is: ${env.NODE_NAME}"   
properties([pipelineTriggers([githubPush(), pollSCM('*/2 * * * *')])])    
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
