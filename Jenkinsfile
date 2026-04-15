pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
                git 'https://github.com/skbehera24/addressbook-v1.git'
            }
        }
          stage('compilitation the code') {
            steps {
                sh 'mvn compile'
            }
        }
         stage('code review') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }
         stage('Unit test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('package') {
            steps {
                sh 'mvn package'
            }
        }
         stage('Code coverage') {
            steps {
                sh 'mvn verify'
            }
        }
        stage('s3 bucket storing') {
            steps {
              s3Upload acl: 'Private', bucket: '', cacheControl: '', file: 'target/*.war', text: 'jenkins-s3-artifact-store-project'
            }
        }
         
    }
}
