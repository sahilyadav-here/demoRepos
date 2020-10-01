pipeline { 
    agent any  
    stages { 
        stage('validate') { 
            steps { 
               sh '''   
               cd demo
               mvn validate
               '''
            }
        }
         stage('Compile') { 
            steps { 
               sh '''
               cd demo
               mvn compile
               '''
            }
        }
        stage('Test') { 
            steps { 
               sh '''
               cd demo
               mvn test
               '''
            }
        }
        stage("build & SonarQube analysis") {
            agent any
            steps {
              withSonarQubeEnv('sonarkube') {
                  sh 'cd demo'
                sh 'mvn clean package sonar:sonar'
              }
            }
          }
        stage('Install') { 
            steps { 
               sh '''
               cd demo
               mvn install
               '''
            }
        }
    }
}
