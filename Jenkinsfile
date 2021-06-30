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
                    def NexusRepo = Version.endsWith("SNAPSHOT") ? "my-devops-lab-SNAPSHOT" : "my-devops-lab-RELEASE"
                        // script below created with snippet generator in Jenkins
                        // varables declared above in "environment" block
                    nexusArtifactUploader artifacts: [[
                            artifactId: "${ArtifactId}", 
                            classifier: '', 
                            file: "target/${ArtifactId}-${Version}.war", 
                            type: 'war'
                    ]], 
                    credentialsId: '374b7981-16d8-437e-9666-0b5e419b97d0', 
                    groupId: "${GroupId}", 
                    nexusUrl: '54.215.219.233:8081', 
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
                sshPublisher(publishers: 
                [sshPublisherDesc(
                    configName: 'Ansible_Controller', 
                    transfers: [
                        sshTransfer(
                            cleanRemote: false,
                            execCommand: 'ansible-playbook /opt/playbooks/downloadanddeploy.yaml -i /opt/playbooks/hosts',
                            execTimeout: 120000
                        ) 
                    ], 
                    usePromotionTimestamp: false, 
                    useWorkspaceInPromotion: false, 
                    verbose: false)])
            }
        }
    }    
}