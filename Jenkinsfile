pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building petclinic freestyle'
                build 'petclinic-freestyle'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing jacoco'
                jacoco exclusionPattern: '**/src/main/java', inclusionPattern: '**/*.class'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying petclinic copyArtifact'
                build 'patclinic-copyArtifact'
            }
        }
    }
}

