pipeline {
    agent any

    environment {
        BUILD_VERSION = '1.0.0'
        STAGE_SUMMARY = ''
    }

    tools {
        nodejs "NodeJS" // Ensure NodeJS is configured in Jenkins
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out the code...'
                script {
                    STAGE_SUMMARY += '- Checkout Code: Success\n'
                }
            }
            post {
                failure {
                    script {
                        STAGE_SUMMARY += '- Checkout Code: Failed\n'
                        error('Stopping pipeline at Checkout Code')
                    }
                }
            }
        }

        stage('Build Application') {
            steps {
                echo 'Building the application...'
                script {
                    error('Simulating Build Failure') // Intentional failure
                }
            }
            post {
                success {
                    script {
                        STAGE_SUMMARY += '- Build Application: Success\n'
                    }
                }
                failure {
                    script {
                        STAGE_SUMMARY += '- Build Application: Failed\n'
                        error('Stopping pipeline at Build Application')
                    }
                }
            }
        }
    }

    post {
        always {
            script {
                def emailBody = """
                Jenkins Job: ${currentBuild.fullDisplayName}
                Status: ${currentBuild.currentResult}

                Stage Status Summary:
                ----------------------
                ${STAGE_SUMMARY}
                """
                echo "Email Body:\n${emailBody}"

                try {
                    // Send email
                    emailext subject: "Jenkins Job: ${currentBuild.fullDisplayName} - Status: ${currentBuild.currentResult}",
                             body: emailBody,
                             to: '2022853154@student.uitm.edu.my'
                } catch (Exception e) {
                    echo "Error while sending email: ${e.message}"
                }
            }
        }

        success {
            echo 'Pipeline completed successfully.'
        }

        failure {
            echo 'Pipeline encountered errors.'
        }
    }
}
