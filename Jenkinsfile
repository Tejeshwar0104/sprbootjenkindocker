pipeline {
  agent any
  tools {
    jdk 'Java17'
    maven 'Maven'
  }
  stages {
    stage('Checkout Code') {
      steps {
        echo 'Pulling from Github'
        git branch: 'main', credentialsId: 'git.tej', url: 'https://github.com/Tejeshwar0104/jenkintrial.git'
      }
    }
    stage('Build Project') {
      steps {
        echo 'Building Java project'
        bat 'mvn clean package -DskipTests'
      }
    }
    stage('Build the Docker Image') {
      steps {
        echo 'Building Docker Image'
        bat 'docker build -t sprbootjenkin:1.0 .'
      }
    }
    
    stage('Run Docker Container') {
      steps {
        echo 'Running SprBoot Application'
        bat '''
        docker rm -f sprbootjenkin-container || exit 0
        docker run --name sprbootjenkin-container sprbootjenkin:1.0
        
        '''               
      }
    }
  }
  post {
    success {
      echo 'BUild and Run is SUCCESSFUL!'
    }
    failure {
      echo 'OOPS!!! Failure.'
    }
  }
}
