pipeline {
    agent any

    stages {

        stage('MAVEN CLEAN') {
            steps {
                sh 'mvn clean'
            }
        }
        stage('MAVEN COMPILE') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('MAVEN SONARQUBE') {
            steps {
                sh 'mvn sonar:sonar -Dsonar.login=squ_a0d08a213d3150623d90598bab2760dca76030e7'
            }
        }
        
    }
}
