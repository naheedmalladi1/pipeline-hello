pipeline
{
    agent any
    stages
    {
        stage('scm checkout')
        {
            steps
            {
        git branch: 'master', url: 'https://github.com/wasim-sajan/maven-project'
            }
        }
        stage('compile the code')
        {
            steps
            {
                withMaven(jdk: 'LocalJDK', maven: 'LocalMaven')
                {
                sh 'mvn compile'
                }
            }
        }  
        stage('Test the code')
        {
            steps
            {
                withMaven(jdk: 'LocalJDK', maven: 'LocalMaven') 
                {
                sh 'mvn test'
                }
            }
        } 
        stage('Build the code')
        {
            steps
            {
                withMaven(jdk: 'LocalJDK', maven: 'LocalMaven')
                {
                sh 'mvn package'
                }
            }
        }  
        stage('Deploy the code')
        {
            steps
            {
                sshagent(['tomcat-deploy-ssh']) 
                {
                   sh 'scp -o StrictHostKeyChecking=no */target/*.war ec2-user@172.31.10.121:/var/lib/tomcat/webapps'
                }
            }
        }     
    }
}
