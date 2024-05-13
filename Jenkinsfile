pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn surefire-report:report'
            }
        }
        stage('Generate Javadoc') {
            steps {
                sh 'mvn javadoc:jar'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'target/surefire-reports/*', fingerprint: true
            archiveArtifacts artifacts: 'target/javadoc.jar', fingerprint: true
        }
    }
}
