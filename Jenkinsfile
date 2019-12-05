pipeline {

    agent any
    
    

    stages {

        stage('Build') {
            steps {
                sh '''
                    mvn -B -DskipTests clean package
                   '''
            }

            post {
                success {
                   archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                }
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }

            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('containarize') {
            steps {
                sh '''
					cd ~
					docker build -t karthik258/maven_app .
				'''
            }
        }

        
    }
}
