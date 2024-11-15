node {
    def app

    stage('clone repository') {


        checkout scm
    }
    stage('Build image') {
      app=docker.build("sherinmonbiju/kubernetescode")
    }
    stage('Test image') {
        app.inside {
            sh 'echo "Tests passed"'
        }
    }
    stage('Push image') {
        docker.withRegistery('https://hub.docker.com/repository/docker/sherinmonbiju/kubernetescode','dockerhub') {
            app.push("${env.BUILD_NUMBER}")
        }
    }
    stage('Trigger ManifestUpdate') {
          echo"triggering Updatemanifestjob"
          build job: 'Updatemanifest' , parameters: [strin(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
        }
    }
