pipeline{
    //Directives
    agent any
    tools {
       maven 'maven'
    }

    environment{
        ArtifactId = readMavenPom().getArtifactId()
        Version = readMavenPom().getVersion()
        Name = readMavenPom().getName()
        GroupId = readMavenPom().getGroupId()
    }
    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }

    // Stage3 : Publish the artefacts  to Nexus
            stage ('Publish to Nexus'){
                steps {
                   script{
                    
                  def NexusRepo = Version.endsWith("SNAPSHOT") ? "ddskDevopsLab-SNAPSHOT" : "dskDevopsLab-RELEASE"

                   nexusArtifactUploader artifacts: 
                   [[artifactId: "${ArtifactId}", 
                   classifier: '',
                   file: 'target/VinayDevOpsLab-0.0.4-SNAPSHOT.war', 
                   type: 'war']], 
                   credentialsId: 'c1f992e3-d7a1-4090-af74-05409399bc14',
                   groupId: "${GroupId}",
                   nexusUrl: '3.137.142.24:8081',
                   nexusVersion: 'nexus3',
                   protocol: 'http', 
                   repository: "${NexusRepo}", 
                   version: "${Version}"
                 }
            }
        }
      // Stage 4 :Print some information 
                stage ('Print some information Variables'){
                    steps {
                       echo "Artifact ID is '${ArtifactId}'"
                       echo "Version is '${Version}'"
                       echo "GroupId is '${GroupId}'"
                       echo "Name is  '${Name}'"
                    }
                }
        // Stage3 : Publish the source code to Sonarqube
        // stage ('Sonarqube Analysis'){
        //     steps {
        //         echo ' Source code published to Sonarqube for SCA......'
        //         withSonarQubeEnv('sonarqube'){ // You can override the credential to be used
        //              sh 'mvn sonar:sonar'
        //         }

        //     }
        // }
        stage ('Deploy'){
            steps {
                echo ' deploying.....'
       
                }

            }
        }
  }
        