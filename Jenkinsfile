pipeline {
    agent any

    stages {
        stage('Checkout GIT') {
            steps {

                echo 'Pulling...';
                git branch: 'main',
                url : 'https://github.com/ferielhakim/tpachat.git',

            }

        }

        
      stage('MVN CLEAN'){
            steps {
                sh 'mvn clean'
            }
        }

        stage('MVN COMPILE') {
            steps{
                sh 'mvn compile'
            }
        }
	    
        
                stage('MVN TEST') {
            steps{
                sh 'mvn test -e '
            }
        }  
        		stage('MVN SONARQUBE') {
            steps {
                sh 'mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=sonar'
            }
        }
        
        stage('NEXUS') {
            steps {
                sh 'mvn deploy -DskipTests'
                  
            }
        }
         stage('Build Docker image Backend') {
            steps {
                sh 'docker build -t ferielhakim/projetdevopsbackend . '
                 
            }
        }
        stage('Login Dockerhub') {

			steps {
			sh 'docker login -u ferielhakim -p 181JFT1565'
			}
			}
        stage('Push image Backend to Dockerhub') {
            steps {
                sh 'docker push ferielhakim/projetdevopsbackend'
                 
            }
        }
        

    }

}

