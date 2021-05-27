pipeline {
    
    agent any//is a directive. run the pipeline for any agent
    tools  {
        maven 'maven'
    }

    stages {
        //stage 1
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }
        //stage 2
        stage ('Test') {
            steps {
                echo 'testing'
            }            
        }

        //stage 3
        stage('Deploy') {
            steps {
                echo 'deploying'
            }
        }
    }
}
