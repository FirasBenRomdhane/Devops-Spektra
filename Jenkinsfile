pipeline {
    agent any

    tools {
        maven 'M2_HOME'
    }

    stages {

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
                sh 'docker start sonarqube'
                sleep 5
                sh 'mvn sonar:sonar -Dsonar.login=squ_b45a8d05b375317a7950a487b3935e32ec9572da'
            }
        }
    }
}