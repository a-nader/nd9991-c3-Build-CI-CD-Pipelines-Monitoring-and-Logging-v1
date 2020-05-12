pipeline {
     agent any
     stages {
         stage('Build') {
             steps {
                 sh 'echo "Hello World NEW"'
                 sh '''
                     echo "Multiline shell steps works too NEW@@@@@"
                     ls -lah
                 '''
             }
         }
         stage('Lint HTML') {
              steps {
                  sh 'tidy -q -e *.html'
              }
         }
         stage('Security Scan') {
              steps { 
                 aquaMicroscanner imageName: 'alpine:latest', notCompliesCmd: 'exit 1', onDisallowed: 'fail', outputFormat: ''
              }
         }         
         stage('Upload to AWS') {
              steps {
                  withAWS(region:’us-east-1’,credentials:’blueocean’) {
                  sh 'echo "Uploading content with AWS creds"'
                      s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'devopsjenkins')
                  }
              }
         }
     }
}
