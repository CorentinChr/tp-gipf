pipeline {
  agent any

  stages {
      stage('Checkout') {
          steps {
              echo "Récupération du code source"
              git branch: 'master', url: 'https://github.com/CorentinChr/tp-gipf'
          }
      }

      stage('Run Tests') {
          steps {
              echo "Lancement des tests avec Gradle"
              sh './gradlew -Dhttps.proxyHost=proxy1-rech -Dhttps.proxyPort=3128 test'
          }
      }
    }
}
