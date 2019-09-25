pipeline {
  agent any
  environment {
    PATH = '/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games:/snap/bin:/var/lib/jenkins/jdk1.8.0_221/bin:/var/lib/jenkins/apache-ant-1.10.5/bin:/var/lib/jenkins/apache-maven-3.6.2/bin'
    JAVA_HOME = '/var/lib/jenkins/jdk1.8.0_221'
  }

  stages {
    stage('Test') {
      steps {
	sh 'ant test'
      }
    }
    stage('Build') {
      steps {
        sh 'ant build'
      }
    }
    stage('Archive') {
      steps {
         archiveArtifacts '**/*.jar'
      }
    }
    stage('Publish_reports') {
      steps {
        junit '**/TEST-*.xml'
      }
    }
    stage('Deploy') {
      steps {
        sh 'cp target/*.jar /tmp'
      }
    }
    stage('Fingerprint') {
      steps {
        fingerprint '**/*.jar'
      }
    }
  }
}

