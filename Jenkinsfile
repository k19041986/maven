node('master')
{
	stage('continuos download') 
	{
	    git 'https://github.com/k19041986/maven'
	}
    stage('continuos build') 
	{
		sh 'mvn package'
    }
    stage('continuous deployment')
    {
	    sh 'scp /home/vagrant/.jenkins/workspace/Pipeline/webapp/target/webapp.war vagrant@192.168.61.22:/var/lib/tomcat7/webapps/qaenv.war'
	}
    stage('continuous testing')
    {
		git 'https://github.com/k19041986/TestingLinux'
		sh 'java -jar /home/vagrant/.jenkins/workspace/Pipeline/testing.jar'	
    }
	stage('continuous Delivery')
    {
		input message :'waiting for approvals for delivery', submitter: 'dem'
		sh 'scp /home/vagrant/.jenkins/workspace/Pipeline/webapp/target/webapp.war vagrant@192.168.61.13:/var/lib/tomcat7/webapps/prodenv.war'	
    }
}