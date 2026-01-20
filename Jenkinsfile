pipeline {
    agent any
    tools {
        // Install the Maven version configured as "M2" and add it to the path.
        maven "M2"
    }

    stages {
        stage('Compile') {
            steps {
                sh "mvn clean compile"
            }
        }
        stage('SonarQube Analysis') {
            environment {
                SONAR_TOKEN = credentials('SONAR_TOKEN')
            }
            steps {
                sh "mvn sonar:sonar -Dsonar.projectKey=vilas-chavan-ST1 -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=${SONAR_TOKEN}"
            }   
        } 
        stage('Build') {
            steps {
                sh "mvn clean package"
            }

            post {
                success {
                    archiveArtifacts 'target/*.war'
                }
            }
        }
    }
}
