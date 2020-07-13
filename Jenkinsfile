pipeline {
     agent any
     stages {
         stage('Build') {
             steps {
                 sh 'echo "Hello World"'
                 sh '''
                     echo "Multiline shell steps works too"
                     ls -lah
                 '''
             }
         }
         stage('Lint HTML') {
              steps {
                  sh 'tidy -q -e *.html'
              }
         }
         stage('Upload to AWS') {
              steps {
                  withAWS(region:'us-west-2',credentials:'aws-static') {
                  sh 'echo "Uploading content with AWS creds"'
                      s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'fancy-static-website-in-aws')
                  }
              }
         }
         stage('Check Website is available') {
              steps {
                  sh 'curl http://fancy-static-website-in-aws.s3-website.us-west-2.amazonaws.com/'
              }
         }
     }
}
