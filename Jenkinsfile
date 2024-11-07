pipeline {
  agent any
  stages {
    stage('SCM') {
      steps {
        git(url: 'https://github.com/yogesh-4297/gitrepo2/', branch: 'main', credentialsId: '3424598f-5a5b-4881-b5f5-1bb0cd4933bd')
      }
    }

    stage('Build&Publish') {
      steps {
        sh '''sudo docker build -t yogesh4297/srepo1:latest .
sudo docker push yogesh4297/srepo1:latest'''
      }
    }

    stage('Deploy') {
      parallel {
        stage('DeployDev') {
          steps {
            sh '''sudo docker rm -f $(sudo docker ps -aq)||true
sudo docker run -d -p 7777:80 --name devcon1 yogesh4297/srepo1:latest'''
          }
        }

        stage('DeployQA') {
          steps {
            sh ''' sudo docker rm -f $(sudo docker ps -aq)||true
 sudo docker run -d -p 9999:80 --name qacon1 yogesh4297/srepo1:latest'''
          }
        }

      }
    }

  }
}