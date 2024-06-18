pipeline{
    agent any

    stages{
        stage('Zip the file'){
            steps{
                sh 'rm -rf *.zip || echo'
                sh 'zip ansible-${BUILD_ID}.zip * --exclude Jenkinsfile'
                sh 'ls -l'
            }
        }
        stage('Upload artifact to jfrog'){
            steps{
                sh 'curl -uadmin:AP6Bdwx4zuzatzGgcxgbkd8vYRm -T \
                ansible-${BUILD_ID}.zip \
                "http://ec2-100-26-165-97.compute-1.amazonaws.com:8081/artifactory/ansible/ansible-${BUILD_ID}.zip" '
            }
        }
        stage('Publish to ansible server'){
            steps{
                sshPublisher(publishers: [sshPublisherDesc(configName: 'ansible server',\
                 transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'ls',\
                  execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: \
                  false, patternSeparator: '[, ]+', remoteDirectory: '.', remoteDirectorySDF: \
                  false, removePrefix: '', sourceFiles: 'ansible-${BUILD_ID}.zip')], usePromotionTimestamp: false,\
                   useWorkspaceInPromotion: false, verbose: false)])
            }
        }
    }
}