pipeline {
  agent any
  stages {
    stage('Github Pull') {
      parallel {
        stage('Github Pull') {
          steps {
            echo 'Pulling from git'
            echo "Git version is $GIT_VER"
            git 'https://github.com/devops-max/simple-java-maven-app'
          }
        }

        stage('Test-1') {
          steps {
            sh 'echo \'Hello test-1\''
          }
        }

      }
    }

    stage('Maven Build') {
      steps {
        echo 'Building Project'
        sh 'mvn clean package'
      }
    }

    stage('Create Docker Image') {
      steps {
        sh 'docker build . -t sampleapp:${VERSION}'
      }
    }

  }
  environment {
    GIT_VER = getSCMVer()
    IMAGE = readMavenPom().getArtifactId()
    VERSION = readMavenPom().getVersion()
  }
}