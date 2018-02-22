pipeline {
  agent {
    node {
      label 'react-node'
    }
    
  }
  stages {
    stage('Build') {
      agent {
        node {
          label 'react-node'
        }
        
      }
      steps {
        git(url: 'https://github.com/Nykaa/nykaa_fe.git', branch: 'master', credentialsId: 'lokesh-github')
        sh 'pwd'
        sh 'node -v'
        sh 'npm install'
        echo 'Running npm install'
      }
    }
    stage('zip-artefact') {
      steps {
        sh 'tar -cvzf /tmp/react-artefact/react-${env.BUILD_NUMBER}.tar.gz ./'
        echo 'zipping artefact'
      }
    }
    stage('upload-artefact') {
      steps {
        pwd(tmp: true)
        echo 'uploading artefact to S3'
        sh 'aws s3 /tmp/artefact.tar.gz s3://raghu-repo'
      }
    }
  }
}