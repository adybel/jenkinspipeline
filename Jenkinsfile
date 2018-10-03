pipeline {
    agent any
    stages {
        stage('Build'){
            steps {
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

