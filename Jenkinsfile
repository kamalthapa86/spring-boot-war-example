pipeline{
    agent any
    tools {
        maven 'Maven3.9.9'
    }
    stages{
        stage("Test"){
            steps{
                //mvn test
                sh "mvn test"
                
            }
            
        }
        
        stage("Build"){
            steps{
                //mvn install
                sh "mvn package"
                
            }
            
        }

        stage("TestServer Deployment"){
            steps{
                // deploy on TestServer
                deploy adapters: [tomcat9(credentialsId: 'tomcat9details', path: '', url: 'http://172.17.0.3:8080')], contextPath: '/app', war: '**/*.war'
                
            }
            
        }

        stage("DeployServer Deployment"){
            steps{
                // deploy on Deployement
                deploy adapters: [tomcat9(credentialsId: 'tomcat9details', path: '', url: 'http://172.17.0.4:8080')], contextPath: '/app', war: '**/*.war'
                
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
