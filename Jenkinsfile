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
                        sudo aws s3 cp $WORKSPACE/target/WebApp.war s3://test1235898
                    '''
             }
         }
        stage ('Restarting application') {
            steps {
                 sh '''
                      ssh -i /home/ec2-user/test.pem ec2-user@54.88.179.127 'aws s3 cp s3://test1235898/WebApp.war /opt/tomcat9/webapps/
                    '''
             }
         }
    }
}
