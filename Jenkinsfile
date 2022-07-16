pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/agehma/sat16july.git'
                    }
                    catch (Exception e1)
                    {
                        mail bcc: '', body: 'unable to download code from github repository', cc: '', from: '', replyTo: '', subject: 'download failed', to: 'gt@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                script
                {
                    try
                    {
                        sh 'mvn package'
                    }
                    catch (Exception e2)
                    {
                        mail bcc: '', body: 'mvn failed to build artifact from code', cc: '', from: '', replyTo: '', subject: 'mvn failed', to: 'devt@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
                script
                {
                    try
                    {
                        deploy adapters: [tomcat9(credentialsId: '752f12ec-a680-4386-b665-fb804faffad9', path: '', url: 'http://172.31.91.123:8080')], contextPath: 'testapp', war: '**/*.war'
                    }
                    catch (Exception e3)
                    {
                        mail bcc: '', body: 'artifact not deployed to container', cc: '', from: '', replyTo: '', subject: 'dc failed', to: 'mwt@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/agehma/testingscript1.git'
                        sh 'java -jar /var/lib/jenkins/workspace/DP-EH/testing.jar'
                    }
                    catch (Exception e4)
                    {
                        mail bcc: '', body: 'selenium failed to test artifact', cc: '', from: '', replyTo: '', subject: 'selenium failed', to: 'st@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousDelivery')
        {
            steps
            {
                script
                {
                    try
                    {
                       deploy adapters: [tomcat9(credentialsId: '752f12ec-a680-4386-b665-fb804faffad9', path: '', url: 'http://172.31.85.56:8080')], contextPath: 'prodapp', war: '**/*.war' 
                    }
                    catch (Exception e5)
                    {
                        mail bcc: '', body: 'delivery failed into prodserver', cc: '', from: '', replyTo: '', subject: 'delivery failed', to: 'dt@gmail.com'
                        exit(1)
                    }
                }
            }
        }
    }
}

