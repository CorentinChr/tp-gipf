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

      stage('Run Sonarqube') {
          steps {
              echo "Lancement de Sonarqube"
              sh './gradlew sonar \
                  -Dsonar.projectKey=TPControle \
                  -Dsonar.projectName='TPControle' \
                  -Dsonar.host.url=http://localhost:9000 \
                  -Dsonar.token=sqp_804a32de64e2e160f8b97c1235e37cbd861180cb'
          }
      }
    
    }
}
