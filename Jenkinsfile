pipeline {
    agent any

    tools {
        maven 'M2_HOME'
    }

    stages {

        stage('Initialize') {
            steps {
                echo '[*] Starting Containers'
                sh 'docker start sonarqube'
                sh 'docker start nexus'
                sleep(30)
            }
        }

        stage('Checkout Code') {
            steps {
                echo '[*] Checking out code from Git'
                git url: 'https://github.com/FirasBenRomdhane/Devops-Spektra.git', branch: 'abdessalem_mami'
            }
        }

        stage('Clean & Compile') {
            steps {
                echo '[*] Cleaning and Compiling Maven Project'
                sh 'mvn clean'
                sh 'mvn compile'
            }
        }

        stage('SonarQube') {
            steps {
                echo '[*] Running SonarQube Analysis'
                sh 'mvn sonar:sonar -Dsonar.login=squ_b45a8d05b375317a7950a487b3935e32ec9572da'
            }
        }

        stage('Deploy with Nexus') {
            steps {
                echo '[*] Deploying Project Artifact to Nexus Repository'
                sh 'mvn deploy'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo '[*] Building Docker Image'
                sh "docker build -t abdessalemmami/achat-app:1.0.0 ."
            }
        }

        stage('Push to Docker Hub') {
            steps {
                echo '[*] Pushing Docker Image to Docker Hub'
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                        sh "docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD"
                        sh "docker push abdessalemmami/achat-app:1.0.0"
                    }
                }
            }
        }

        stage('Run App with Docker Compose') {
            steps {
                echo '[*] Running App with Docker Compose'
                sh 'docker compose up -d'
            }
        }

        stage('Prometheus'){
            steps {
                echo '[*] Running Prometheus'
                sh 'docker start prometheus'
            }
        }

        stage('Grafana'){
            steps {
                echo '[*] Running Grafana'
                sh 'docker start grafana'
            }
        }

    }

    post {
        success {
            emailext subject: "Pipeline Success: ${currentBuild.fullDisplayName}",
                      body: 'The pipeline completed successfully. No further action is required.',
                      to: 'mami.abdessalem@gmail.com'
        }

        failure {
            emailext subject: "Pipeline Failure: ${currentBuild.fullDisplayName}",
                      body: 'The pipeline has failed. Please check the Jenkins logs for more information.',
                      to: 'mami.abdessalem@gmail.com'
        }
    }
}