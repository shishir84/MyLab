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
        stage ('Static Code Analysis using Sonar') {
            steps{
                 withSonarQubeEnv("SonarQube") { // You can override the credential to be used
                    sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
                 }

            }
        }
        // //stage 4
        // stage ('Publish') {
        //     steps {
        //         script {
                    
        //             def Nex = Version.endsWith("SNAPSHOT") ? "VinaysDevOpsLab-SNAPSHOT" : "VinaysDevOpsLab-RELEASE"
                    
        //             nexusArtifactUploader artifacts: 
        //             [[artifactId: "${ArtifactId}", 
        //             classifier: '', 
        //             file: "target/${ArtifactId}-${Version}.war", 
        //             type: 'war']], 
        //             credentialsId: 'nexus-cred', 
        //             groupId: "${GroupId}", 
        //             nexusUrl: '172.20.10.13:8081', 
        //             nexusVersion: 'nexus3', 
        //             protocol: 'http', 
        //             repository: "${Nex}", 
        //             version: "${Version}"
        //         }               
        //     }
        // }
        // //stage 5
        // stage('Deploy to Tomcat') {
        //     steps {
        //         sshPublisher(publishers: [sshPublisherDesc(configName: 'Ansible-Controller', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'ansible-playbook /home/ansibleadmin/playbook/downloadanddeploy.yaml -i /home/ansibleadmin/playbook/hosts', execTimeout: 1200000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
        //     }
        // }

        //  //stage 6
        // stage('Deploy to Docker') {
        //     steps {
        //         sshPublisher(publishers: [sshPublisherDesc(configName: 'Ansible-Controller', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'ansible-playbook /home/ansibleadmin/playbook/downloadanddeploy_docker.yaml -i /home/ansibleadmin/playbook/hosts', execTimeout: 1200000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
        //     }
        // }
    }
}