pipeline{
    // Directives
    agent any
    tools {
        maven 'maven'
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
        // stage 2.5 - Publish the artifacts to Nexus
        stage('Publish to Nexus') {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.0.4-snapshot.war', type: 'war']], credentialsId: '5c5108be-e9bc-4cb8-b9df-f21fd10fbe3c', groupId: 'com.vinaysdevopslab', nexusUrl: '172.20.10.235:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'EstonDevopsLab-SNAPSHOT', version: '0.0.4-snapshot'
            }
        }

        // stage 3 - deploying
        stage ('Deploy') {
            steps {
                echo 'deploying. . .'
            }
        }
    }
}