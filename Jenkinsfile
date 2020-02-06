pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
            {
                sh "mvn clean verify -DrunUnitTests=true -DbuildNumber=${env.BUILD_NUMBER}"
                script{
                currentBuild.result = 'SUCCESS'
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                cifsPublisher(publishers: [[configName: 'Automic', transfers: [[cleanRemote: false, excludes: '', flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: 'target/', sourceFiles: 'target/*.war']], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false]])
                createDepPckg appName: 'DIGITALBANK', folder: 'DEFAULT', owner: '100/AUTOMIC/AUTOMIC', pass: 'AUTOMIC', pkgName: '$BUILD_NUMBER', pkgType: 'Deployment', server: 'http://10.0.0.228:80/cda', useCentlCrd: true, user: '100/AUTOMIC/AUTOMIC'
                execApplnWkf appName: 'DIGITALBANK', executeAt: '', installationMode: 'overwrite', manualConfirmation: 'no', pass: 'AUTOMIC', pkgName: '$BUILD_NUMBER', profile: 'DEV', queue: '', server: 'http://10.0.0.228:80/cda', startAt: 'now', useCentlCrd: true, user: '100/AUTOMIC/AUTOMIC', userGroup: '', workflow: 'DeployDigitalBank'
                sendNotificationToCDD appName: 'Digital-Bank', appVersion: 'V1', releaseTokens: '{"DBankBuildNumber":"$BUILD_NUMBER"}'
            }
        }
    }
}
