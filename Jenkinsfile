pipeline {
    agent any

    tools {
        maven 'MAVEN-HOME'
    }

    stages {

        stage('Checkout') {
            steps {
                git url: 'https://github.com/aishwarya9887/war-web-project.git',
                    branch: 'master'
            }
        }

        stage('Build with Maven') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Archive WAR') {
            steps {
                archiveArtifacts artifacts: '**/target/*.war',
                    fingerprint: true
            }
        }
    }

    post {
        success {
            emailext(
                subject: "Jenkins Build Successful: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                    <h2>Jenkins Build Successful</h2>
                    <p>Job: ${env.JOB_NAME}</p>
                    <p>Build Number: ${env.BUILD_NUMBER}</p>
                    <p>Status: SUCCESS</p>
                """,
                to: 'aishuwarya1231@gmail.com'
            )
        }

        failure {
            emailext(
                subject: "Jenkins Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                    <h2>Jenkins Build Failed</h2>
                    <p>Job: ${env.JOB_NAME}</p>
                    <p>Build Number: ${env.BUILD_NUMBER}</p>
                    <p>Status: FAILURE</p>
                """,
                to: 'aishuwarya1231@gmail.com'
            )
        }
    }
}
