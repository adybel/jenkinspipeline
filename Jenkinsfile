pipeline {
    agent any
    tools{
        maven 'localMvn'
    }
    stages {
        stage('Build'){
            steps {
                echo 'mvn clean package'
                bat 'mvn clean package'
                }
            post {
                success {
                    echo "Now archiving..."
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to Staging') {
            steps {
                build job: 'deploy-to-staging'
            }
        }
        stage ('Deploy to Production'){
            steps {
                build job 'deploy-to-prod'
            }
            post {
                success{
                    echo 'Code deployed to Production'
                }
                failure {
                    echo 'Deployment FAILED'
                }
            }
        }
    }

//git add Jenkinsfile
//git commit -m "add Jenkinsfile"
//git push

}

