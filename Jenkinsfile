pipeline {
    agent any

    stages {
        stage('GIT') {
            steps {
               echo "Getting project from git";
                checkout([$class: 'GitSCM', branches: [[name: 'rima_ibri']], userRemoteConfigs: [[url: 'https://github.com/FirasBenRomdhane/Devops-Spektra.git']]])
            }
        }
      
        stage('MVN CLEAN') {
            steps {
                echo "Getting started with MVN clean";
                sh 'mvn clean'
            }
        }

        stage('MVN COMPILE') {
            steps {
                echo "Getting started with MVN compile";
                sh 'mvn compile'
            }
        }
        
       stage('MVN SonarQube') {
            steps {
          
                 sh 'mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=sonar'
                

                }
            }
        }
    }    
