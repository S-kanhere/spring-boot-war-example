pipeline{
    agent any
    tools {
        maven 'MAVEN3' 
    }

    stages{
        stage("Test"){
            steps{
                // mvn test
                sh "mvn --version"
            }
        }

        stage("Build"){
            steps{
                sh "mvn package"  
            }
        }

        stage("Deploy on test"){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat9details', path: '', url: 'http://3.110.33.1:8080')], contextPath: '/app', war: '**/*.war'
            }
        }

        stage("Deploy on prod"){
            input{
                message "Should we continue"
                ok "yes we should"
            }
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat9details', path: '', url: 'http://13.234.231.41:8080')], contextPath: '/app', war: '**/*.war'
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
