pipeline {
    agent any
    tools {
        maven 'maven'
    }
    
    stages {
        stage("Clean up") {
            steps {
                deleteDir()
            } // Fermer cette accolade pour `steps`
        } // Fermer cette accolade pour `stage`
        
        stage("Clone repo") {
            steps {
                sh 'git clone https://github.com/SassiMotaz/backend-master.git'
            }
        }
        
        stage("Generate backend image") {
            steps {
                dir("backend-master") {
                    sh 'mvn clean install'
                    sh 'docker build -t backend .'
                }
            }
        }
        
        stage("Run backend compose") {
            steps {
                dir("backend-master") {
                    sh 'docker-compose up -d'
                }
            }
        }
    } // Fermer cette accolade pour `stages`
} // Fermer cette accolade pour `pipeline`
