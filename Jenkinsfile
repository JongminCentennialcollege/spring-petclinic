pipeline {
    agent any
    triggers {
        cron('H/10 * * * 1')
    }
    stages {
        stage('Build') {
            steps {
                script {
                    def mvnHome = tool 'M3'
                    sh "${mvnHome}/bin/mvn -Dmaven.test.failure.ignore clean package"
                }
            }
        }
        stage('Test and Report') {
            steps {
                script {
                    def mvnHome = tool 'M3'
                    sh "${mvnHome}/bin/mvn test"
                    sh "${mvnHome}/bin/mvn jacoco:report"
                }
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            jacoco()
        }
    }
}
