pipeline {
    
    agent any//is a directive. run the pipeline for any agent
    tools  {
        maven 'maven'
    }

    environment {
       ArtifactId = readMavenPom().getArtifactId()
       Version = readMavenPom().getVersion()
       Name = readMavenPom().getName()
       GroupId = readMavenPom().getGroupId()
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
                script {
                    
                    def Nex = Version.endsWith("SNAPSHOT") ? "VinaysDevOpsLab-SNAPSHOT" : "VinaysDevOpsLab-RELEASE"
                    
                    nexusArtifactUploader artifacts: 
                    [[artifactId: "${ArtifactId}", 
                    classifier: '', 
                    file: "target/${ArtifactId}-${Version}.war", 
                    type: 'war']], 
                    credentialsId: 'nexus-cred', 
                    groupId: "${GroupId}", 
                    nexusUrl: '172.20.10.13:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: "${Nex}", 
                    version: "${Version}"
                }               
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