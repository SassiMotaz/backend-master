pipeline {
    agent any
    tools {
        maven 'maven_3_9_6' // Utiliser le nom correct de l'installation Maven
    }
    
    stages {
        stage("Clean up") {
            steps {
                deleteDir()
            }
        }
        
        stage("Clone repo") {
            steps {
                script {
                    if (isUnix()) {
                        sh 'git clone https://github.com/SassiMotaz/backend-master.git'
                    } else {
                        bat 'git clone https://github.com/SassiMotaz/backend-master.git'
                    }
                }
            }
        }
        
        stage("Generate backend image") {
            steps {
                dir("backend-master") {
                    script {
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
        
        stage("Run backend compose") {
            steps {
                dir("backend") {
                    sh 'docker-compose up '
                }
            }
        }
    }
}
