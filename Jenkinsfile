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
                    message: "Build Started: ${env.JOB_NAME} ${env.BUILD_NUMBER} ${env.GIT_BRANCH} ${env.BRANCH_NAME} ${env.GIT_COMMIT} by ${BUILD_USER} (<${env.BUILD_URL}|Open>)"
            }
        }
            
        stage('Build steps'){
            steps {
                sh '''
                echo "hi prince"
                '''
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
                message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} by ${BUILD_USER}\n More info at: ${env.BUILD_URL}"
        }
    }
}
