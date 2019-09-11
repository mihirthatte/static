pipeline{
  agent any
  stages{
    stage('Upload to AWS'){
      steps{
        withAWS(credentials:'aws-static') {
          s3Upload(file:'index.html',
                   bucket:'jenkins-bucket-mihir',
                   path:'index.html')
        }
        sh 'echo "Hello World"'
      }
    }
  }
}
