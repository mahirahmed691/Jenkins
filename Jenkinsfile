
def groovy 

pipeline {
    agent any 
    
    parameters{
        choice(name: 'VERSION', choices:['1.1.0', '1.2.0', '1.3.0'], description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: '' )
    }
    
    stages{

        stage ("init"){
             agent{
                     docker {
                            image 'gradle:6.7-jdk11'
                            // Run the container on the node specified at the top-level of the Pipeline, in the same workspace, rather than on a new node entirely:
                             reuseNode true
                        }
                }
            steps{
                script {
                    sh "whoami"
                    sh 'gradle --version'
                    echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
                    groovy = load "script.groovy"
                }
            }
        }

        stage ("build"){
            steps{
                script {
                    groovy.buildApp()
                }
            }
        }
        stage ("test"){           
            steps{
                 script{
                     groovy.testApp()
                 }
            }
        }
        stage ("deploy"){
            steps{
                script {
                    groovy.deployApp()
                }
                
            }
        }
    }
}