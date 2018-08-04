pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy to Staging'){
            steps{
                build job: 'deploy-to-staging-8888'   
            }
        }
        stage ('Deploy to production'){
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message: 'Approve production'
                }
                build job: 'deploy-to-8899'
            }
            post {

                success {
                    echo 'Code has been deployed to production'
                }
                failure {

                    echo 'Failure in the pipeline'
                }

            }
        }
    }
}
