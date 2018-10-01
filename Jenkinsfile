pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/selenium-saikrishna/maven.git'
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
                sh 'scp /home/ubuntu/.jenkins/workspace/Pipeline/webapp/target/webapp.war ubuntu@172.31.34.195:/var/lib/tomcat7/webapp/qaenv.war'
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                git 'https://github.com/selenium-saikrishna/TestingOnAWS.git'
            
                
            }
        }
        
    }
    post
    {
        success
        {
            input message: 'Waiting for Approval', submitter: 'Venu'
             sh 'scp /home/ubuntu/.jenkins/workspace/Pipeline/webapp/target/webapp.war ubuntu@172.31.47.219:/var/lib/tomcat7/webapp/prodenv.war'
        }
        failure
        {
            mail bcc: '', body: 'Jenkins job has failed', cc: '', from: '', replyTo: '', subject: 'Jenkins Notification', to: 'gandham.saikrishna@gmail.com'
        }
    }
}

