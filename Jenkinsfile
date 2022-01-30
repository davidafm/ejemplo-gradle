pipeline {
    agent any
    environment {
        NEXUS_USER         = credentials('NEXUS-USER')
        NEXUS_PASSWORD     = credentials('NEXUS-PASS')
    }
    parameters {
        choice choices: ['maven', 'gradle'], 
        description: 'Seleccione una herramienta para proceder a compilar', 
        name: 'CompileTool'
    }
    stages {
        stage("Pipeline"){
            steps {
                script{
                    if(params.CompileTool=='maven'){
                        //compilar con maven
                        def executor = load 'maven.groovy'
                        executor.call()
                    }else{
                        //compilar con gradle
                        def executor = load 'gradle.groovy'
                        executor.call()
                    }
                }
            }
             post{
                success{
                    slackSend color: 'good', message: "[David Figueroa] [${JOB_NAME}] [${BUILD_TAG}] Ejecucion Exitosa", teamDomain: 'dipdevopsusac-tr94431', tokenCredentialId: 'token-slack'
                }
                failure{
                    slackSend color: 'danger', message: "[David Figueroa] [${env.JOB_NAME}] [${BUILD_TAG}] Ejecucion fallida en stage [${env.TAREA}]", teamDomain: 'dipdevopsusac-tr94431', tokenCredentialId: 'token-slack'
                }
            }
        }
    }
}
