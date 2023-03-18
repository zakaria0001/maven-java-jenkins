pipeline {
    agent any
    tools { 
      maven 'MAVEN_HOME' 
      jdk 'JAVA_HOME' 
    }
    stages {
        stage('Build') {
            steps {
                 sh 'mvn compile'        
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Package') {
            steps {
                sh 'mvn package'            
            }
            post {
              always {
                junit 'target/surefire-reports/*.xml'
              }
              success{
                  archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
              }
            }
        }
        stage('Deploy'){
            steps{
                withEnv(['JENKINS_NODE_COOKIE=dontKillMe']){
                   sh 'nohup java -jar -DServer.port=8001 /Users/mbp-de-zakaria/Documents/JenkinsTestProject/spring-petclinic/target/spring-petclinic-3.0.0-SNAPSHOT.jar &'
                }
            }
        }
    }
}
