@Library("dpope-shared-libraries") _
pipeline {
  
//   environment {
//      DOCKER_TAG = getVersion()
//    }
  
  agent {
    kubernetes {
      label 'promo-app'  // all your pods will be named with this prefix, followed by a unique id
      idleMinutes 5  // how long the pod will live after no jobs have run on it
      yamlFile 'build-pod.yaml'  // path to the pod definition relative to the root of our project 
      defaultContainer 'maven'  // define a default container if more than a few stages use it, will default to jnlp container
    }
  }
  stages {
    stage('Build') {
      steps {  // no container directive is needed as the maven container is the default
        helloWorld()
        sh "mvn clean package"   
      }
    }
    stage('Build Docker Image') {
      steps {
        container('docker') {     
                //sh "docker build -t shbali/promo-app:dev ."
                //sh " docker run -dp 3000:3000 shbali/promo-app:dev "
           }
        //container(name: 'kaniko', shell: '/busybox/sh') {
         // sh '''#!/busybox/sh
          //  echo "FROM jenkins/inbound-agent:latest" > Dockerfile
         //   /kaniko/executor --context `pwd` --destination shbali/hello-kaniko:latest 
         // '''
       //  }
          
          
         // sh "docker build -t shbali/promo-app:dev ." 
          
          //withCredentials([string(credentialsId: 'docker-hub', variable: 'dockerHubPwd')]) {
          //      sh "docker login -u shbali -p ${dockerHubPwd}"
           // } 
          
         // sh "docker push shbali/promo-app:dev"        // which is just connecting to the host docker deaemon
        
        //}
      }
    }
  }
}

def getVersion(){
    def commitHash = sh label: '', returnStdout: true, script: 'git rev-parse --short HEAD'
    return commitHash
}
