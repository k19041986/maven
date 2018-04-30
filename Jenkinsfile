//Changes done for the jenkins file

node('master') 
{
    stage('ContinuousDownload')
    {
        git 'https://github.com/k19041986/maven'
    }
    
    
    stage('ContinuousBuild') 
    {
        sh '''
          mvn package'''
    }
    
    stage('ContinuousDeployment') 
    {
        sh 'scp /var/lib/jenkins/workspace/CodeasPipeline/webapp/target/webapp.war vagrant@192.168.61.22:/var/lib/tomcat7/webapps/qaenv.war'
    }
    
    stage('ContinuousTesting')
    {
        
        git 'https://github.com/k19041986/TestingLinux'
        
        sh 'java -jar /var/lib/jenkins/workspace/CodeasPipeline/testing.jar'
        
    }
    
    stage('ContinuousDelivery')
    {
        input message: 'Waiting for approval for delivery from Delivery manager', submitter: 'dem'
        sh 'scp /var/lib/jenkins/workspace/CodeasPipeline/webapp/target/webapp.war vagrant@192.168.61.13:/var/lib/tomcat7/webapps/prodenv.war'
    }
    
    

    
    
    
    
}

