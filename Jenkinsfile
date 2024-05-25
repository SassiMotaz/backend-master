pipeline {
    agent any
    tools {
        // Ensure the Maven tool name matches the one configured in Jenkins global tools configuration
        maven 'maven_3_9_6'
    }
    
    stages {
        stage('Clean up') {
            steps {
                // Clean the workspace to ensure no residual files affect the build
                deleteDir()
            }
        }
        
        stage('Clone repo') {
            steps {
                script {
                    // Clone the repository; use sh for Unix and bat for Windows
                    if (isUnix()) {
                        sh 'git clone https://github.com/SassiMotaz/backend-master.git'
                    } else {
                        bat 'git clone https://github.com/SassiMotaz/backend-master.git'
                    }
                }
            }
        }
        
        stage('Generate backend image') {
            steps {
                dir('backend-master') {
                    script {
                        // Build the Maven project and create a Docker image
                        if (isUnix()) {
                            sh 'mvn clean install'
                            sh 'docker build -t backend .'
                        } else {
                            bat 'mvn clean install'
                            bat 'docker build -t backend .'
                        }
                    }
                }
            }
        }
        
        stage('Run backend compose') {
            steps {
                dir('backend-master') {
                    // Use docker-compose to start the services
                    // Make sure docker-compose.yml is in the 'backend-master' directory
                    script {
                        if (isUnix()) {
                            sh 'docker-compose up -d'
                        } else {
                            bat 'docker-compose up -d'
                        }
                    }
                }
            }
        }
    }
}
