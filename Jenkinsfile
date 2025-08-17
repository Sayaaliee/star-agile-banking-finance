pipeline{
  agent any
  stages{
    stage('Build Project'){
      steps{
        git url: 'https://github.com/Sayaaliee/star-agile-banking-finance/', branch: "master"
        sh 'mvn clean package'

     }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t sayaalieee/staragileprojectfinance:v6 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push sayaalieee/staragileprojectfinance:v5'
                }
            }
        }
        
     stage('Deploy') {
            steps {
                    sh 'sudo docker run -itd -p 8083:83 sayaalieee/staragileprojectfinance:v6'
                    
                }
            }
        }
    }
