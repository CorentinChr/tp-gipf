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
              sh './gradlew -Dhttps.proxyHost="proxy1-rech" -Dhttps.proxyPort=3128 test'
          }
      }

      stage('Build') {
          steps {
            echo "Build du projet"
            sh './gradlew -Dhttps.proxyHost="proxy1-rech" -Dhttps.proxyPort=3128 compileJava'
          }
      }

    
      stage('Run Sonarqube') {
          steps {
              echo "Lancement de Sonarqube"
              sh './gradlew -Dhttps.proxyHost="proxy1-rech" -Dhttps.proxyPort=3128 sonar \
                  -Dsonar.projectKey=tp \
                  -Dsonar.projectName="tp" \
                  -Dsonar.host.url=http://172.17.0.1:9000 \
                  -Dsonar.token=sqp_ce3212db5c33d3d53335643be75c6c724131602d'
          }
      }

      stage('Create jar') {
          steps {
              echo "Construction du jar"
              sh './gradlew -Dhttps.proxyHost="proxy1-rech" -Dhttps.proxyPort=3128 jar'
          }
      }

    stage('Release') {
        steps {
            archiveArtifacts artifacts: 'build/libs/**/*.jar'
        }
    }



    
    }
}
