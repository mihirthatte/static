pipeline{
  agent any
  stages{
    stage('Lint HTML'){
      steps{
        sh 'tidy -q -e *.html'
      }
    }
    stage('Upload to AWS'){
      steps{
        withAWS(credentials:'aws-static') {
          s3Upload(file:'index.html',
                   bucket:'jenkins-bucket-mihir',
                   path:'index.html')
        }
      }
    }
    stage('Validate S3 has HTML file'){
      steps{
        script{
          def status_code = sh returnStdout: true,
                             script: ' curl -s -o /dev/null -w "%{http_code}" http://jenkins-bucket-mihir.s3-website.us-east-2.amazonaws.com/abc.html'
          echo "Status code is -- $status_code"
          if (status_code != "200"){
            echo "hereeeeee"
            currentBuild.result = "FAILURE"
          }
        }
      }
    }
  }
}
