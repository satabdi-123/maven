pipeline
{
  agent any
  stages
  {
    stage('ContinuousDownload')
    {
      steps
      {
       git 'https://github.com/intelliqittrainings/maven.git'
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
       deploy adapters: [tomcat9(credentialsId: 'c6b951f6-e0e6-41e1-ab7a-c9744494c742', path: '', url: 'http://172.31.88.42:8080')], contextPath: 'testapp', war: '**/*.war'
      }
    }
    stage('ContinuousTesting')
    {
        steps
        {
         git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
         sh 'java -jar /var/lib/jenkins/workspace/ScriptedPipeline/testing.jar'
        }
    }
    stage('ContinuousDelivery')
    {
        steps
        {
         deploy adapters: [tomcat9(credentialsId: 'c6b951f6-e0e6-41e1-ab7a-c9744494c742', path: '', url: 'http://172.31.83.18:8080')], contextPath: 'prodapp', war: '**/*.war'
        }
    }
  }
}
