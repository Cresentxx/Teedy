pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test' // Runs the tests and generates the Surefire report
            }
        }
        stage('Generate Javadoc') {
            steps {
                sh 'mvn javadoc:jar' // Generates the Javadoc
            }
        }
        stage('pmd') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }
    }
    post {
        always {
            // Archive Surefire reports and Javadoc
            archiveArtifacts artifacts: '&zwnj;**/target/surefire-reports/**&zwnj;', fingerprint: true
            archiveArtifacts artifacts: '&zwnj;**/target/site/apidocs/**&zwnj;', fingerprint: true
            
            // Keep the existing artifact archiving
            archiveArtifacts artifacts: '&zwnj;**/target/**&zwnj;/*.jar', fingerprint: true
            archiveArtifacts artifacts: '&zwnj;**/target/**&zwnj;/*.war', fingerprint: true
        }
    }
}
