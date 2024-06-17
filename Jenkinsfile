pipeline{
    agent any

    stages{
        stage('zip the file'){
            steps{
                sh 'zip ansible-${BUILD_ID}.zip * --exclude Jenkinsfile'
                sh 'ls -l'
            }
        }
        stage('upload artifact to jfrog'){
            steps{
                sh 'curl -uadmin:AP6Bdwx4zuzatzGgcxgbkd8vYRm -T \
                ansible-${BUILD_ID}.zip \
                "http://ec2-100-26-165-97.compute-1.amazonaws.com:8081/artifactory/ansible/ansible-${BUILD_ID}.zip" '
            }
        }
    }
}