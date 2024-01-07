pipeline {
  agent any
  stages {
      stage ('test') { // la phase build is
                  steps {
                      bat './gradlew.bat test'
                      archiveArtifacts 'build/test-results/'
                      cucumber reportTitle: 'Cucumber report',
                      fileIncludePattern: 'target/report.json',
                      trendsLimit: 10,
                      classifications: [
                          [
                             'key': 'Browser',
                              'value': 'Firefox'
                          ]
                      ]
                      junit 'build/test-results/test/TEST-Matrix.xml'
                  }
      }
      stage ('Code Analysis') { // la phase build hh
                  steps {
                                      withSonarQubeEnv('sonar'){
                      bat './gradlew.bat sonarqube'
                                      }
                  }
      }
}

}