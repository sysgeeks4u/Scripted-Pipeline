node('built-in') 
{
    stage('Continuous Download') 
    {
      git branch: 'main', url: 'https://github.com/sysgeeks4u/Maven-Tomcat.git'

     try
     {
        sh 'mvn package'  //This might Fail

     }

     catch (Exception e)
     {
      echo "Build is Faild"
      // Email Notification

      mail bcc: '', body: 'CI CD & CD Faild', cc: 'rnraju4u@gmail.com', from: '', replyTo: '', subject: 'CI_CD_Process', to: 'ram.ashokit@gmail.com'
      exit(1)
     }

    git branch: 'main', url: 'https://github.com/sysgeeks4u/Maven-Tomcat.git'
    }

    stage('Continuous Build') 
    {
    sh 'mvn package'
    }

    stage('Continuous Deployment') 
    {
    deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcattest', path: '', url: 'http://172.31.24.35:8080')], contextPath: 'testapp', war: '**/*.war'
    }
    
    stage('Continuous Test') 
    {
    git branch: 'main', url: 'https://github.com/sysgeeks4u/Functional-Testing.git'

    sh 'java -jar /var/lib/jenkins/workspace/Scripted-Pipeline/testing.jar'
    }
    
    stage('Continuous Delivery') 
    {
    deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcatprod', path: '', url: 'http://172.31.68.42:8080')], contextPath: 'prodapp', war: '**/*.war'
    }
}

