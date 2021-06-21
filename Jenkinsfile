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

        // stage 3 - deploying
        stage ('Deploy') {
            steps {
                echo 'deploying. . .'
            }
        }
    }
}