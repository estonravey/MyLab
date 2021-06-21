pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
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

        // Stage3 : Publish the source code to Sonarqube
        stage ('Sonarqube Analysis'){
            steps {
                echo ' Source code published to Sonarqube for SCA......'
                withSonarQubeEnv('sonarqube'){ // You can override the credential to be used
                     sh 'mvn sonar:sonar'
                }
            }
<<<<<<< HEAD
        }       
    }
}

/*
must be enclosed within the pipeline block {}
- Directives: agent, tools, environment, etc

Stages --> stage --> steps

agent: execute this pipeline on any avaialable agents
- locate an executor
- create a workspace for entire pipeline
- need a tools sections: preinstall tools or add tool to path 

STAGES ( 3 stages)
-GUILD
sh (execute shell command) 'mvn clean install package'

-TEST


-DEPLOY





*/
=======
        }        
    }
}
>>>>>>> b724c4a5c1251509e8a809365245ef24b21cbd09
