pipeline {
    agent any
    
    tools {
        maven 'maven'
    }
    
    stages {
        stage('code') {
            steps {
                git url: 'https://github.com/piyushgarg362-commits/jenkins-java-project.git'
            }
        }
        stage('build') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('artifact') {
            steps {
                sh 'mvn package'
            }
        }
               stage('s3') {
            steps {
                withAWS(region: 'ap-south-1', credentials: 'my-aws-s3-key') {
                    s3Upload(
                        file: 'target/NETFLIX-1.2.2.war', 
                        bucket: 'artifactbucketfornetflixapp'
                    )
                }
            }
        }

        stage('deploy') {
            steps {
                // Your deployment shell scripts or commands go here
                echo 'Deploying application...'
           }
        }
    } 
} 
