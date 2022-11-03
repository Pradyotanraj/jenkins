pipeline{
    agent any
    tools{
        maven 'local_maven'
    }
    stages{
        stage ('Build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                sucess{
                    echo "Archiving the Artifacts"
                    archiArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to tomcat server') {
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat-users', path: '', url: 'http://35.78.205.99:8081/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}