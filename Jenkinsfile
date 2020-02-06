pipeline {
    agent any

    stages {
        stage('Deploy') {
            steps {
               sendNotificationToCDD appName: 'Digital-Bank', appVersion: 'V1', releaseTokens: '{"DBankBuildNumber":"$BUILD_NUMBER"}'
            }
        }
    }
}
