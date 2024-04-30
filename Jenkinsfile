pipeline {
    agent any
	
	tools {
    jdk 'java-1.8'

  }

    stages {
        stage('CLONE SCM') {
            steps {
                echo 'Cloning GAME OF LIFE project code'
				git 'https://github.com/ShruthiJohara/game-of-life.git'

            }
        }

stage('Build Artifact ') {
            steps {
                echo 'generating artifact with maven build tool'
				sh 'mvn  compile'
            }
        }



	    
		stage('SONARqube ANALYSIS') {
            steps {
                echo 'code inspection of  GAME OF LIFE project code'
			    sh '''mvn sonar:sonar \\
  -Dsonar.host.url=http://54.89.117.143:9000 \\
  -Dsonar.login=755d6290f70aabc3f0d6da73c33e5a2c5d6784a2'''
			    
            }
        }
		
		
		stage('Build Artifact ') {
            steps {
                echo 'generating artifact with maven build tool'
				sh 'mvn  install'
            }
        }
		
		stage('Deploy to tomcat') {
            steps {
                echo 'Deploying artifact to tomcat webserver '
				deploy adapters: [tomcat9(credentialsId: '80459988-41e8-44f0-b42f-f47712085d30', path: '', url: 'http://54.236.24.75:8081/')], contextPath: 'Gameoflife', war: '*/*.war'
            }
        }
    }
}
