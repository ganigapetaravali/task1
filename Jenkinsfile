pipeline {
  environment {
    registry = "18.212.25.74:8001/repository/k8s-task/"
    registryCredential = 'nexus'
    dockerImage = ''	  
    }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git branch: 'main', url: 'https://github.com/ganigapetaravali/task.git'
      }
    }
   stage('Building image') {
      steps{
        script {
          sh 'docker build -t flask:2.0 .'
        }
       }
	  }
    stage('Deploy Image in to nexus registry') {
      steps{
        script {
	   //sh 'curl "admin:ravali" -X PUT http://18.212.25.74:8001/repository/k8s-task/flask:2.0 '
		//flask:2.0.push("latest")
          sh 'docker tag flask:2.0 18.212.25.74:8001/repository/k8s-task/flask:2.0'
          //sh 'docker login -u ravali1505 -p Manoj@123@123'
	  sh 'docker login 18.212.25.74:8001/repository/k8s-task/' 
          sh 'docker push 18.212.25.74:8001/repository/k8s-task/flask:2.0'
          sh 'docker logout http://18.212.25.74:8001/repository/k8s-task/'
            }
          }
        }
      }
    }
