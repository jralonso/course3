<<<<<<< HEAD
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
    stage('Security Scan') {
        steps { 
            aquaMicroscanner imageName: 'alpine:latest', notCompliesCmd: 'exit 1', onDisallowed: 'fail', outputFormat: 'json'
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
=======
pipeline {
  agent any
  stages {
    stage('AWS Credentials') {
      steps {
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'blueocean', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
        sh """  
               mkdir -p ~/.aws
               echo "[default]" >~/.aws/credentials
               echo "[default]" >~/.boto
               echo "aws_access_key_id = ${AWS_ACCESS_KEY_ID}" >>~/.boto
               echo "aws_secret_access_key = ${AWS_SECRET_ACCESS_KEY}">>~/.boto
               echo "aws_access_key_id = ${AWS_ACCESS_KEY_ID}" >>~/.aws/credentials
               echo "aws_secret_access_key = ${AWS_SECRET_ACCESS_KEY}">>~/.aws/credentials
        """
        }
      }
    }
    stage('Create EC2 Instance') {
      steps {
        ansiblePlaybook playbook: 'main.yaml', inventory: 'inventory'
      }
    }
  }
}
>>>>>>> 8e6522fe55c40af9f8912bbe02795e97ef91204b
