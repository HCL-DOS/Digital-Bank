pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
            {
                sh "mvn clean verify -DrunUnitTests=true -DbuildNumber=${env.BUILD_NUMBER}"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
               sendNotificationToCDD appName: 'Digital-Bank', appVersion: 'V1', releaseTokens: '{"DBankBuildNumber":"$BUILD_NUMBER"}'
            }
        }
    }
}
