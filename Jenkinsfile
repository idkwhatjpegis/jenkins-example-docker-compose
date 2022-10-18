pipeline {
  agent any
  def remote = [:]
    remote.name = 'docker1'
    remote.host = 'docker1.do1.lab'
    remote.user = 'jenkins'
    remote.password = 'admin'
    remote.allowAnyHosts = true
  stages {
    stage("verify tooling") {
      steps {
        sh '''
          docker version
          docker info
          docker compose version 
          curl --version
          jq --version
        '''
      }
    }
    stage('Docker Compose test') {
      steps {
        sh 'docker compose config'
      }
    }
    stage('Docker Compose Build') {
      steps {
        sh 'docker compose build'
        
      }
    }
    stage('Docker Compose Up') {
      steps {
        sh 'docker compose up -d'
      }
    }
  }
  post {
    always {
      sh 'docker compose ps'
    }
  }
}
