pipeline {
    agent any
    tools{
        maven: 'localMvn'
    }
    stages {
        stage('Build'){
            steps {
                echo 'mvn clean package'
                sh 'mvn clean package'
                }
            post {
                success {
                    echo "Now archiving..."
                    archiveArtifacts artifacts: '**/targetr/*.war'
                }
            }
        }
       
    }

//git add Jenkinsfile
//git commit -m "add Jenkinsfile"
//git push

}

