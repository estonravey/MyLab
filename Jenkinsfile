pipeline{
    // Directives
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
        // specify various stages within stages
        // stage 1 - build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // stage 2 - testing
        stage ('Test') {
            steps {
                echo ' testing ...'
            }
        }

        // stage 3 - Publish the artifacts to Nexus
        stage('Publish to Nexus') {
            steps {
                script {
                    def NexusRepo = Version.endsWith("SNAPSHOT") ? "EstonDevopsLab-SNAPSHOT" : "EstonDevopsLab-RELEASE"

                    nexusArtifactUploader artifacts: 
                    [[artifactId: "${ArtifactId}", 
                    classifier: '', 
                    file: "target/${ArtifactId}-${Version}.war",  
                    type: 'war']], 
                    credentialsId: '5c5108be-e9bc-4cb8-b9df-f21fd10fbe3c', 
                    groupId: "${GroupId}", 
                    nexusUrl: '172.20.10.235:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: "${NexusRepo}", 
                    version: "${Version}"
                }
            }
        }

        // stage 4 -print some information 
        stage ('Print Environment Variables') {
            steps {
                echo "Artifact ID is '${ArtifactId}'"
                echo "Version is '${Version}'"
                echo "GroupID is '${GroupId}'"
                echo "Name is '${Name}'"
            }
        }

        // stage 5 - deploying
        stage ('Deploy') {
            steps {
                echo 'deploying. . .'
            }
        }
    }
}