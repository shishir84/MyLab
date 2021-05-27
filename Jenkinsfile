pipeline {
    
    agent any//is a directive. run the pipeline for any agent
    tools  {
        maven 'maven'
    }

    environment {
        groupId = readMavenPom().getGroupId()
        artifactId = readMavenPom().getArtifactId
        version = readMavenPom().getVersion()
        name = readMavenPom().getName
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
        stage ('Publish') {
            steps {
                nexusArtifactUploader artifacts: 
                [[artifactId: "${artifactId}", 
                classifier: '', 
                file: 'target/VinayDevOpsLab-0.0.4-SNAPSHOT.war', 
                type: 'war']], 
                credentialsId: 'nexus-cred', 
                groupId: "${groupId}", 
                nexusUrl: '172.20.10.13:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: 'VinaysDevOpsLab-SNAPSHOT', 
                version: "${version}"
            }
        }
        //stage 4
        stage('Deploy') {
            steps {
                echo 'deploying'
            }
        }
    }
}