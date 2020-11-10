pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        withEnv(overrides: ["JAVA_HOME=${ tool 'JDK 8' }", "PATH+MAVEN=${tool 'Maven'}/bin:${env.JAVA_HOME}/bin"]) {
        sh 'mvn -f apiops-anypoint-jenkins-sapi/pom.xml clean install -Dtestfile=runner.TestRunner.java -DskipTests'
      }
    }
    }
    stage('Munit') {
      steps {
        sh 'mvn -f apiops-anypoint-jenkins-sapi/pom.xml test'
      }
    }
     
   stage('Deploy') {
      steps {
        withEnv(overrides: ["JAVA_HOME=${ tool 'JDK 8' }", "PATH+MAVEN=${tool 'Maven'}/bin:${env.JAVA_HOME}/bin"]) {
          sh 'mvn -f apiops-anypoint-jenkins-sapi/pom.xml clean package deploy -DmuleDeploy -Dtestfile=runner.TestRunner.java -Danypoint.username=joji4 -Danypoint.password=Canadavisa25@ -DapplicationName=apiops-anypoint-jenkins-joji -Dcloudhub.region=us-east-2'
        }

      }
    }
    stage('FunctionalTesting') {
      steps {
        
        withEnv(overrides: ["JAVA_HOME=${ tool 'JDK 8' }", "PATH+MAVEN=${tool 'Maven'}/bin:${env.JAVA_HOME}/bin"]) {
          sh 'mvn -f cucumber-API-Framework/pom.xml test -Dtestfile=/src/test/java/runner.TestRunner.java'
        }

      }
    }
    stage('GenerateReports') {
      steps {
        cucumber(failedFeaturesNumber: -1, failedScenariosNumber: -1, failedStepsNumber: -1, fileIncludePattern: 'cucumber.json', jsonReportDirectory: 'cucumber-API-Framework/target', pendingStepsNumber: -1, skippedStepsNumber: -1, sortingMethod: 'ALPHABETICAL', undefinedStepsNumber: -1)
      }
    }

    stage('fetch properties') {
      steps {
        script {
          readProps= readProperties file: 'cucumber-API-Framework/email.properties'
          echo "${readProps['email.to']}"
        }

      }
    }

    stage('Email') {
      steps {
        emailext(subject: 'Testing Reports for $PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', body: 'Please find the functional testing reports. In order to check the logs also, please go to url: $BUILD_URL'+readFile("cucumber-API-Framework/emailTemplate.html"), attachmentsPattern: 'cucumber-API-Framework/target/cucumber-reports/report.html', from: "${readProps['email.from']}", mimeType: "${readProps['email.mimeType']}", to: "${readProps['email.to']}")
      }
    }
  }
    
  tools {
    maven 'Maven'
  }
}
