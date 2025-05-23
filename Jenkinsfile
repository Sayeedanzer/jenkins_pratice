pipeline{
        agent any
        tools {
            maven 'Maven' 
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
                    //mvn package
                    sh "mvn package"
                    }
            }
            stage("Deploy on Test"){
                steps{
                    //deploy on container -> plugin
                    deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcatserver_test', path: '', url: 'http://34.126.217.64:8080/')], contextPath: '/app', war: '**/*.war'
                    }
            }
            stage("Deploy on"){
                steps{
                    //deploy on container -> plugin
                    deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcatserver_test', path: '', url: 'http://34.131.255.226:8080/')], contextPath: '/app', war: '**/*.war'     
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
