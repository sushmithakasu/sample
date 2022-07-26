pipeline {
    agent any

    tools {
        maven 'M2_HOME'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        
        stage ('Copy .war file to tomcat') {
             steps {
                 sh '''
                        scp -i /home/ec2-user/test.pem $WORKSPACE/target/WebApp.war ec2-user@54.88.179.127:/home/ec2-user
                    '''
             }
         }
        stage ('Restarting application') {
            steps {
                 sh '''
                      ssh -i /home/ec2-user/test.pem ec2-user@54.88.179.127 'sudo cp /home/ec2-user/WebApp.war /opt/tomcat9/webapps
                    '''
             }
         }
    }
}
