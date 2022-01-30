pipeline {
    agent any
    environment {
        NEXUS_USER         = credentials('NEXUS-USER')
        NEXUS_PASSWORD     = credentials('NEXUS-PASS')
    }
    parameters {
        choice choices: ['maven', 'gradle'], description: 'Seleccione una herramienta para proceder a compilar', name: 'CompileTool'
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
            post {
                always {
                    sh "echo 'fase always executed post'"
                }
                success {
                    sh "echo 'fase success'"
                }
                failure {
                    sh "echo 'fase failure'"
                }
            }
        }
    }
}
