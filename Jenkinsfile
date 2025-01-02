pipeline {
  agent any 
  environment {
    DOCKER_REGISTRY = '<dockerhub-uername>'
    DOCKER_IMAGE = "{DOCKER_REGISTRY}/better"
    AWS_REGION = 'us-east-1'
    SNS_TOPIC_ARN = 'arn:aws:sns:us-east-1:021176216734:Better'
  }
  stages {
    stage('git checkout') {
      steps {
        git branch: 'main', url: '<git repo URL'
      }
    }
    stage("Dependencies installation for node.js app") {
      steps {
        sh 'npm install'
      }
    }
    stage("Run tests") {
      steps {
        sh 'npm test'
      }
    }
    stage("creating docker image") {
      steps {
        sh 'docker build -t better .'
      }
    }
    stage("pushing to dockerhub") {
      steps {
       withCredentials([usernameColonPassword(credentialsId: 'dockercreds', variable: 'dockerhubcreds')]) {
          sh 'docker login -u <Dockerhub-Username> -p $(dockerhubcreds)'
       }
      }
    }
    stage("deploying to K8s") {
      steps {
        withKubeConfig(caCertificate: '', clusterName: 'Master', contextName: '', credentialsId: '', namespace: '', restrictKubeConfigAccess: false, serverUrl: 'https://k8s-cluster-server URL') {
          sh """ 
          kubectl apply -f deployment.yml
          kubectl apply -f service.yml
          """
        }
      }
    }
  }
  post {
    success {
      steps {
        withAWS(credentials: 'aws-credentials', region: AWS_REGION) {
          sh """
          aws sns publish --topic-arn $SNS_TOPIC_ARN --message 'Deployment succeeded for Node.js application.'
          """
        }
      }
    }
    failure {
      steps {
        withAWS(credentials: 'aws-credentials', region: AWS_REGION) {
          sh """
          aws sns publish --topic-arn $SNS_TOPIC_ARN --message 'Deployment failed for Node.js application.'
          """
        }
      }
    }   
  }
}

      
        
    
     
        
