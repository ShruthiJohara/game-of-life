pipeline {
    agent any

    stages {

        stage(‘cloning git repo') {
            steps {
                echo ‘Cloning git repo’
git 'https://github.com/ShruthiJohara/game-of-life.git'

            }
        }



stage(‘Sonar-code quality') {
            steps {
                echo ‘Checking ode quality’
sh '''mvn sonar:sonar \\
  -Dsonar.host.url=http://54.89.117.143:9000 \\
  -Dsonar.login=755d6290f70aabc3f0d6da73c33e5a2c5d6784a2'''

            }
        }



stage(‘mvn clean package’) {
            steps {
                echo ‘generating Artifacts’
sh '''mvn clean package’’’

            }
        }


stage(‘Tomcat deploy’) {
            steps {
                echo ‘Deploy artifact to tomcat’
  deploy adapters: [tomcat9(credentialsId: '80459988-41e8-44f0-b42f-f47712085d30', path: '', url: 'http://54.236.24.75:8081/')], contextPath: 'Gameoflife', war: '*/*.war'
            }
        }

}

}
