pipeline{
    agent any

    stages{
        stage('Zip the File'){
            steps{
                sh 'rm -rf *.zip || echo'
                sh 'zip -r ansible-${BUILD_ID}.zip * --exclude Jenkinsfile'
                sh 'ls -l'
            }
        }
        stage('Upload Artifact to jfrog'){
            steps{
                sh 'curl -uadmin:AP6Bdwx4zuzatzGgcxgbkd8vYRm -T\
                 ansible-${BUILD_ID}.zip\
                  "http://ec2-34-229-56-41.compute-1.amazonaws.com:8081/artifactory/ansible/ansible-${BUILD_ID}.zip"'
            }
        }
        stage('Publish to Ansible Server'){
            steps{
                sshPublisher(publishers: [sshPublisherDesc(configName: 'ansible server',\
                 transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'unzip -o ansible-${BUILD_ID}.zip; rm -rf ansible-${BUILD_ID}.zip',\
                  execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false,\
                   patternSeparator: '[, ]+', remoteDirectory: '.', remoteDirectorySDF: false, removePrefix: '',\
                    sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
    }
}