node {
  stage 'Checkout'
  git url: 'https://github.com/russmckendrick/jenkins-docker-example.git'

  stage ('build') {

    withCredentials([[
      $class: 'UsernamePasswordMultiBinding',
      credentialsId:'docker-hub-credentials',
      usernameVariable: 'USERNAME',
      passwordVariable: 'PASSWORD'
      ]]) {
        app = docker.build("${USERNAME}/mobycounter")
    }
  }

  stage 'deploy'
  sh './deploy.sh'
  
  stage('push') {
    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
      app.push('latest');
    }
  }
}