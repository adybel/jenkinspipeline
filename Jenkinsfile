pipeline {
    agent any

    parameters {
         string(name: 'tomcat_dev', defaultValue: 'localhost:8081', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: 'localhost:8090', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *')
     }

stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        bat "copy -i /home/jenkins/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/apache-tomcat/apache-tomcat-8.5.34-staging/webappss"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        bat "copy -i /home/jenkins/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/apache-tomcat-8.5.34-prod/webapps"
                    }
                }
            }
        }
    }
}
