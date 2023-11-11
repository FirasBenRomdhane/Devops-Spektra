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
        
        stage('SonarQube Analysis') {
            steps {
                 sh 'mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=sonar'
                }
            }
            
        stage('Nexus') {
            steps {
            sh 'mvn deploy -DskipTests'
            }
        }
            
        stage('Building image'){
            steps {
                    sh "docker build -t rimaibri/achat:1.0.0 ."
                            
            }
        }
        
        stage('Docker Push') {
            steps {
                    
                    script {
                        sh "docker login -u rimaibri -p docker2023/"

                        sh "docker push rimaibri/achat:1.0.0"
                    }
                
            }
        }

        
    }
}    
