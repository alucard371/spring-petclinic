pipeline {
    agent any

    environment {
        CI='true'
    }

    stages {
        stage('checkout code') {
            steps {
            checkout scm
            }
        }
        stage('Build') {


            steps {
                echo 'Building petclinic freestyle'
                build 'petclinic-freestyle'
                echo 'Deploying petclinic copyArtifact'
                build 'patclinic-copyArtifact'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing jacoco'
                jacoco exclusionPattern: '**/src/main/java', inclusionPattern: '**/*.class'
                echo 'Testing junit'
                junit testDataPublishers: [[$class: 'AttachmentPublisher']], testResults: ''
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy step'
            }
        }
    }
}

