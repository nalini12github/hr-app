pipeline{
    agent any
    
    stages{
       
        stage("Maven Build"){
            steps{
                sh 'mvn clean package'
            }
        }
        stage("Tomcat Deploy - Dev"){
            steps{
                sshagent(['slave']) {
                    // Copy war file to tomcat
                    sh "scp -o StrictHostKeyChecking=no target/hr-app.war ec2-user@172.31.8.208:/opt/tomcat9/webapps"
                    sh "ssh ec2-user@172.31.8.208 /opt/tomcat9/bin/shutdown.sh"
                    sh "ssh ec2-user@172.31.8.208 /opt/tomcat9/bin/startup.sh"
                }
            }
        }
    }
}
