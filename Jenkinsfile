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
                //echo 'Building petclinic freestyle'
                //build 'petclinic-freestyle'
                //echo 'Deploying petclinic copyArtifact'
                //build 'patclinic-copyArtifact'

                sh 'mvn -B jacoco:report checkstyle:checkstyle install'
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
                sh 'docker build -t petclinic .'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing jacoco'
                jacoco exclusionPattern: '**/src/main/java', inclusionPattern: '**/*.class'
                echo 'Testing junit'
                junit testDataPublishers: [[$class: 'AttachmentPublisher']], testResults: ''

                jacoco()
                recordIssues(tools: [checkStyle(), junitParser(), mavenConsole()])
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy step'
                sh 'docker stop $(cat .dockerpidfile)'
                sh 'docker run -p 8088:8080 -d petclinic > .dockerpidfile'
            }
        }
    }
}

