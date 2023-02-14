pipeline {
    agent {
        label 'jenkins-slave'
    }
    tools{
        maven 'MAVEN3.8.7'
    }
    options{
        ansiColor('xterm')
    }
    stages{
        /*
        stage('Checkout'){
            steps{
                    //git 'https://github.com/chaithanya1812/pass.git'
                    git branch: "${BRANCH_NAME}", url: 'https://github.com/chaithanya1812/pass.git'
                    echo "\033[1;4;37;42m GIT STAGE IS COMPLETED \033[0m"
            }
        }
        */
    
        stage('Build'){
            steps{
                   sh 'mvn clean package'
            }
        }
        stage('Docker-login'){
            steps{
                   withCredentials([string(credentialsId: 'ddockerloginn', variable: 'dockerlogin')]){
                   sh 'docker login -u chaitu1812 --password ${dockerlogin} || true'
                   echo "\033[1;4;37;42m DOCKER LOGIN STAGE IS COMPLETED \033[0m"
                    }
                }    
            }    
        stage('Docker-Build-Push'){
                steps{
                    script{
                    sh "docker build -t chaitu1812/${BRANCH_NAME} --build-arg branch=${BRANCH_NAME} ."   
                    sh "docker push chaitu1812/${BRANCH_NAME}"
                    sh "docker rmi chaitu1812/${BRANCH_NAME}"
                    echo "\033[1;4;37;42m Docker build and push is completed IS COMPLETED \033[0m"
                    }
           }
        }
      stage('Delete con & Img'){
            steps{
                sh 'docker stop ${BRANCH_NAME} || true'
                sh 'docker rm ${BRANCH_NAME} || true'
                sh 'docker rmi ${BRANCH_NAME} || true'
                sh 'docker rmi $(docker images -q -f dangling=true) || true'
              }
        }
        stage('Run containers'){
            steps{
                sh 'docker run -d --name c2 -p 8091:8080 chaitu1812/${BRANCH_NAME}'   
            }
        }

    } 
}
