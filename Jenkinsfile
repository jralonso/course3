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
        withAWS(region: 'us-west-2', credentials: 'jra-udacity-c3') {
          sh 'echo "Uploading content with AWS creds"'
          s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file: 'index.html', bucket: 'course3-static-jenkins-pipeline-master')
        }

      }
    }

  }
}
