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
      stage ('Code Analysis') { // la phase build
                  steps {
                                      withSonarQubeEnv('sonar'){
                      bat './gradlew.bat sonarqube'
                                      }
                  }
      }
      stage("Quality gate") {
                  steps {
                      waitForQualityGate abortPipeline: true
                  }
      }

      stage("Build") {
              steps {
                  bat './gradlew.bat build'
                  bat './gradlew.bat javadoc'
                  archiveArtifacts 'build/libs/*.jar'
                  archiveArtifacts 'build/docs/'
              }
      }
      stage("deploy") {
                  steps {
                      bat './gradlew.bat publish'

                  }
      }
      stage("notification") {
                  steps {
                       notifyEvents message: 'Pipeline  is sucessufuly termined', token: 'texibiiaiylbshdbuzat-qcmklslouyt'
                       mail bcc: '', body: 'Pipeline <b> is sucessufuly termined</b>', cc: 'ka_boukef@esi.dz', from: '', replyTo: '', subject: 'process Success', to: 'ks_sellami@esi.dz'
                  }
      }

}

}