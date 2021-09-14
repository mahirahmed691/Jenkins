
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
                script{
                    groovy = load "script.groovy"
                }
            }
        }

        stage ("build"){
            steps{
                script{
                    groovy.buildApp()
                }
            }
        }
        stage ("test"){
            when{
                expression {
                    params.executeTests
                }
            }
            steps{
                 script{
                     groovy.testApp()
                 }
            }
        }
        stage ("deploy"){
            steps{
                groovy.deployApp()
            }
        }
    }
}