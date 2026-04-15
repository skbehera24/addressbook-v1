
pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
                git 'https://github.com/skbehera24/addressbook-v1.git'
            }
        }

        stage('compile code') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('code review') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }

        stage('unit test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('code coverage') {
            steps {
                sh 'mvn verify'
            }
        }

        stage('s3 bucket storing') {
            steps {
                s3Upload(
                    bucket: 'jenkins-s3-artifact-store-project',
                    file: 'target/addressbook.war',
                    acl: 'Private'
                )
            }
        }
    }
}
