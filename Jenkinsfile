def COLOR_MAP = [
    'SUCCESS': 'good', 
    'FAILURE': 'danger',
]
def getBuildUser() {
    return currentBuild.rawBuild.getCause(Cause.UserIdCause).getUserId()
}
pipeline {
    // Set up local variables for your pipeline
    environment {
        BUILD_USER = ''
    }

    agent any

    stages {
        stage('Slack Notification'){
            steps {
                script {
                BUILD_USER = getBuildUser()
            }
                slackSend channel: '#jenkins-build',
                          color: '#0000FF',
                    message: "Build Started:\n Job Name: ${env.JOB_NAME}\n Initaited By: ${BUILD_USER}\n Build Number: ${env.BUILD_NUMBER}\n Git Branch: ${env.GIT_BRANCH}\n Git commit ID: ${env.GIT_COMMIT}\n More info at: (<${env.BUILD_URL}|Open>)"
            }
        }
            
        stage('Docker Image Build'){
            steps {
                sh '''
                echo "Docker Image Build"
                '''
            }

                post {
                // only triggered when blue or green sign
                success {
                slackSend channel: '#jenkins-build',
                color: COLOR_MAP[currentBuild.currentResult],
                message: "Docker Image Build Successfull"
                }
                // triggered when red sign
                failure {
                slackSend channel: '#jenkins-build',
                color: COLOR_MAP[currentBuild.currentResult],
                message: "Docker Image Build Failed"
                }
                }

        }
        
         stage('Docker Image Push'){
            steps {
                sh '''
                echo "Docker Image Push"
                '''
            }
                post {
                // only triggered when blue or green sign
                success {
                slackSend channel: '#jenkins-build',
                color: COLOR_MAP[currentBuild.currentResult],
                message: "Docker pushed to ECR Successfull"
                }
                // triggered when red sign
                failure {
                slackSend channel: '#jenkins-build',
                color: COLOR_MAP[currentBuild.currentResult],
                message: "Docker pushed to ECR failed"
                }
                }
            
        }

    }

    // Post-build actions
    post {
        always {
            script {
                BUILD_USER = getBuildUser()
            }
            echo 'I will always say hello in the console.'
            slackSend channel: '#jenkins-build',
                color: COLOR_MAP[currentBuild.currentResult],
                message: "*${currentBuild.currentResult}:* Job Name: ${env.JOB_NAME}\n Initaited By: ${BUILD_USER}\n Build Number: ${env.BUILD_NUMBER}\n Git Branch: ${env.GIT_BRANCH}\n Git commit ID: ${env.GIT_COMMIT}\n  More info at: ${env.BUILD_URL}"
        }
    }
}
