node('built-in') 
{
    stage('Continuous Download') 
    {
    git branch: 'main', url: 'https://github.com/sysgeeks4u/Maven-Tomcat.git'
    }

    stage('Continuous Build') 
    {
    sh 'mvn package'
    }

    stage('Continuous Deployment') 
    {
    deploy adapters: [tomcat9(credentialsId: 'admin', path: '', url: 'http://172.31.24.35:8080')], contextPath: 'test-app', war: '**/*.war'
    }
    
    stage('Continuous Test') 
    {
    git branch: 'main', url: 'https://github.com/sysgeeks4u/Functional-Testing.git'

    sh 'java -jar /var/lib/jenkins/workspace/Scripted-Pipeline/testing.jar'
    }
    
    stage('Continuous Delivery') 
    {
    deploy adapters: [tomcat9(credentialsId: 'admin', path: '', url: 'http://172.31.68.42:8080')], contextPath: 'test-app', war: '**/*.war'
    }
}

