node {

   def registryProjet='registry.gitlab.com/saidmokrani/presentation-jenkins'
   def IMAGE="${registryProjet}:version-${env.BUILD_ID}"

    stage('Clone') {
          git 'https://github.com/saidmokrani/jenkins--build-docke.git'
    }

    def img = stage('Build') {
          docker.build("$IMAGE",  '.')
    }

    stage('Run') {
          img.withRun("--name run-$BUILD_ID -p 80:80") { c ->
            sh 'curl localhost'
          }
    }

    stage('Push') {
          docker.withRegistry('https://registry.gitlab.com', 'reg1' ) {
              img.push 'latest'
              img.push()
          }
    }

}



