pipeline {
  agent {
    docker {
     image 'node:10.18.0'
     args '-p 3000:3000'
    }
  }
  environment {
    CI = 'true'
    HOME = '.'
    npm_config_cache = 'npm-cache'
  }
  stages {
        stage('Install Packages') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }
        stage('Deploy') {
            steps {
                withAWS(region:'us-east-1', credentials:'AWS secrets') {
                    s3Upload(bucket: 'meetup-demo-app', workingDir:'build', path: 'angular_footer', includePathPattern:'**/*');
                }
            }
        }
    }
}