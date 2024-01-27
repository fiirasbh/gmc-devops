pipeline {
    agent any;

    stages {
      stage('Build') {
            steps {
                script {
                    // Checkout the Git repository
                    git branch: 'main',
                    credentialsId: 'fben',
                    url: 'https://github.com/fiirasbh/gmc-devops.git'
                }
            }
        }

        stage("Build Artifact") {
            steps {
                // Build your Maven project, skipping tests
                sh 'mvn clean compile'
                 

                sh 'mvn package -DskipTests'
            }
        }

          stage('TestMOCKITO') {
            steps {
                
                sh 'mvn test'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                // Add this command to execute the SonarQube analysis
                sh 'mvn sonar:sonar -Dsonar.host.url=http://192.168.100.21:9000 -Dsonar.login=admin -Dsonar.password=sonar'
            }
        }

        stage("Nexus") {
            steps {
                sh "mvn deploy -Durl=http://192.168.100.21/repository/maven-releases/ -Drepository.username=admin -Drepository.password=admin -Dmaven.test.skip"
            }
        }

            }
        }
    }
}

