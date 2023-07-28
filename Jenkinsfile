pipeline {
    agent any
    tools {
        maven "MAVEN3"
        jdk "openjdk8"
    }
    stages {
        stage('Fetch code') {
            steps {
                git branch: 'main', url: 'https://github.com/charancherry5887/java.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving it...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy') {
            steps {
                sshagent(['tomcat']) {
                    sh 'scp -o StrictHostKeyChecking=no target/MyWebApp.war ubuntu@172.31.3.212:/opt/tomcat/webapps'
                }
            }
        }
    }
}
