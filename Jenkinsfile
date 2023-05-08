pipeline {
    agent any

    stages {
        stage('docker bui') {
            steps {
                sh 'docker build . -t abhishek00007/lampp:${BUILD_NUMBER}'
                
            }
            
        }
        stage('docker login'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dochub-pwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u abhishek00007 -p ${dockerhubpwd}'
                   
  
}

                }
            }
        }
        stage('docker image push')
        {
            steps
            {
                sh 'docker push abhishek00007/lampp:${BUILD_NUMBER}'
                // sh 'echo feature test'
            }
        }
        stage('Deploy to K8s')
        {
            steps
            {
              withKubeConfig([credentialsId: '0fe6a189-a124-43d0-8fcf-d3f27ac0fa63']) {

              sh 'kubectl apply -f phppod.yml'  
              sh 'kubectl set image deployment/mydeploy mycontainer=abhishek00007/lampp:${BUILD_NUMBER}'
              
              
}
               
            }
        }
    }
}
