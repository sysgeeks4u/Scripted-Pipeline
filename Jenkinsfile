node('built-in')
{
    stage('Continuous Download')
    {
        //It is a repo for continuous download
        git branch: 'main', url: 'https://github.com/sysgeeks4u/Maven-Tomcat.git'
    }

    stage('Continuous Build')
    {
        //execute maven command for building application
        sh 'mvn package'
    }

    stage('Continuous Delivery')
    {
        //Delivering application on a staging servers
        deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'test-admin', path: '', url: 'http://172.31.22.81:8080')], contextPath: 'testapp', war: '**/*.war'
    }

    stage('Continuous Test')
    {
        //Download Testing software from repo
        git branch: 'main', url: 'https://github.com/sysgeeks4u/Functional-Testing.git'

        //Execute testing.jar file
        sh 'java -jar /var/lib/jenkins/workspace/Scripted-Pipeline/testing.jar'
    }

    stage('Continuous Deployment')
    {
        //Deploying application on live servers/prod servers
        deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'prodserver_admin', path: '', url: 'http://172.31.24.228:8080')], contextPath: 'prodapp', war: '**/*.war'
    }
    
}
