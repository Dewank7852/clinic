pipeline {
    agent any
    
    tools {
        jdk 'jdk11'
        maven 'maven3'
    }
    
    stages {
        stage('SCM') {
            steps {
               git branch: 'main', url:'https://github.com/jaiswaladi246/Petclinic.git'
            }
        }
        stage('Code Compile') {
            steps {
                    sh "mvn  compile"
            }
        }
        
        stage('Run Test Cases') {
            steps {
                    sh "mvn test"
            }
        }
        
        stage('Maven Build') {
            steps {
                    sh "mvn clean install"
            }
        }
        
        stage('Docker Build & Push') {
            steps {
                   script {
                       withDockerRegistry(credentialsId: '5912dfcd-8713-46f0-b7a0-d9abcb078082', toolName: 'docker') {
                           sh 'docker build -t test-deploy .'
                           sh 'docker tag test-deploy dewankchauhan7852/deploy-1:latest'
                           sh 'docker push dewankchauhan7852/deploy-1:latest'
                           
                            
                        }
                   } 
            }
        }
        
    }

}
