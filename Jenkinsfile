pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        withEnv(overrides: ["JAVA_HOME=${ tool 'JDK 8' }", "PATH+MAVEN=${tool 'Maven'}/bin:${env.JAVA_HOME}/bin"]) {
          sh 'mvn -f apiops-anypoint-bdd-sapi/pom.xml clean install -Dtestfile=runner.TestRunner.java -DskipTests'
        }

      }
    }

   // stage('Deploy') {
    //  steps {
    //    withEnv(overrides: ["JAVA_HOME=${ tool 'JDK 8' }", "PATH+MAVEN=${tool 'Maven'}/bin:${env.JAVA_HOME}/bin"]) {
     //     sh 'mvn -f apiops-anypoint-bdd-sapi/pom.xml package deploy -DmuleDeploy -Dtestfile=runner.TestRunner.java -Danypoint.username=joji4 -Danypoint.password=Canadavisa25@ -DapplicationName=apiops-bdd-sapi-jo -Dcloudhub.region=us-east-2'
     //   }

<<<<<<< HEAD
      }
    }

=======
     // }
    //}
   
>>>>>>> 64f1f5072636f8a3fa533a729bc2dbf38c985a1e
    //stage('Clone another repository') {
    //  steps {
     //   git branch: 'master',
     //   credentialsId: '87af46ec-e10a-46f3-accd-60bfacb10526',
     //   url: 'https://github.com/jojivarghese25/Cucumber-automation.git'
     // }
   // }
    stage('Checkout code') {
            steps {
                 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CheckoutOption', timeout: 60]], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '6450a696-f924-4a1a-b70f-9e69524dcb53', url: 'https://github.com/jojivarghese25/Cucumber-automation.git']]])
<<<<<<< HEAD

=======
              
>>>>>>> 64f1f5072636f8a3fa533a729bc2dbf38c985a1e
            }
        }

    stage('FunctionalTesting') {
     steps {
       withEnv(overrides: ["JAVA_HOME=${ tool 'JDK 8' }", "PATH+MAVEN=${tool 'Maven'}/bin:${env.JAVA_HOME}/bin"]) {
          sh 'mvn -f cucumber-API-Framework/pom.xml test'
<<<<<<< HEAD
       }

     }
=======
         //-Dcucumber.options="src/test/java/features/ --tags ~@Ignore"'
       
       }
     }
      
>>>>>>> 64f1f5072636f8a3fa533a729bc2dbf38c985a1e
    }

  stage('Cucumber Reports') {
    steps {
              cucumber failedFeaturesNumber: -1, failedScenariosNumber: -1, failedStepsNumber: -1, fileIncludePattern: '**/*.json', jsonReportDirectory: 'cucumber-API-Framework/target/', pendingStepsNumber: -1, reportTitle: 'Reports', skippedStepsNumber: -1, sortingMethod: 'ALPHABETICAL', undefinedStepsNumber: -1
           }
           
        }


<<<<<<< HEAD
    //stage('Email') {
     // steps {
     //   emailext(subject: 'Testing Reports for $PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', body: 'Please find the functional testing reports. In order to check the logs also, please go to url: $BUILD_URL'+readFile("apiops-anypoint-bdd-sapi/emailTemplate.html"), attachmentsPattern: 'apiops-anypoint-bdd-sapi/target/cucumber-reports/report.html', from: "jojisham13@gmail.com", mimeType: "text/html", to: "jojihr@gmail.com")
     // }
  //  }
=======
    stage('Email') {
      steps {
        emailext attachmentsPattern: 'cucumber-API-Framework/target/cucumber-reports/report.html', body: 'please find attached report', replyTo: 'jojisham13@gmail.com', subject: 'Reports', to: 'jojisham13@gmail.com'
      }
    }
>>>>>>> 64f1f5072636f8a3fa533a729bc2dbf38c985a1e

  }
  tools {
    maven 'Maven'
  }
  //post {
  //  failure {
<<<<<<< HEAD
   //   emailext(subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', body: 'Please find attached logs.', attachLog: true, from: "jojisham13@gmail.com", to: "jojihr@gmail.com")
   // }

 // }
}
=======
   //   emailext(subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', body: 'Please find attached logs.', attachLog: true, from: "jojisham13@gmail.com", to: "jojisham13@gmail.com")
   // }

 // }
}

>>>>>>> 64f1f5072636f8a3fa533a729bc2dbf38c985a1e
