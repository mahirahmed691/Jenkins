
def groovy 

pipeline {
    agent any
    
    parameters{
        choice(name: 'VERSION', choices:['1.1.0', '1.2.0', '1.3.0'], description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: '' )
    }
    
    stages{

        stage ("init"){
            steps{
                def dockerHome = tool 'Docker'
                env.PATH = "${dockerHome}/bin:${env.PATH}"
                script {
                    sh "whoami"
                    sh 'mvn -B'
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