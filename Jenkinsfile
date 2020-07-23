pipeline {
    agent any

    agent {
        // Equivalent to "docker build -f Dockerfile.build --build-arg version=1.0.2 ./build/
        dockerfile true
    }

    environment {
        CI='true'
    }

    stages {
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
            }
        }
         stage('Deliver for development') {
                    when {
                        branch 'development'
                    }
                    steps {
                        echo 'development branch'
                        input message: 'Finished using the web site? (Click "Proceed" to continue)'

                    }
                }
         stage('Deploy for production') {
            when {
                branch 'production'
            }
            steps {
                echo 'production branch'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'

            }
        }
    }
}

