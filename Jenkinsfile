pipeline {
    agent {
      dockerfile {
        args '-v /var/run/docker.sock:/var/run/docker.sock -v /Users/shrayansh/docker-ivy/harmony-sbt-cache/ivy2:/root/.ivy2 -v /Users/shrayansh/docker-ivy/harmony-sbt-cache/cache:/root/.cache'
      }
    }
    options {
    ansiColor('xterm')
  }
   stages {
   
   stage('setting build name'){
       steps {
   script {
if (env.BRANCH_NAME.startsWith('PR')) {
    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'shrayansh-global-personal-git', usernameVariable: 'username', passwordVariable: 'pass']]) {
      def resp = httpRequest url: "https://github.com/shrayansh/multi-docker/pulls/${env.BRANCH_NAME.substring(3)}", customHeaders: [[name: 'Authorization', value: "token ${env.pass}"]]
      echo resp
      def ttl = getTitle(resp)
      def itm = getItem(env.BRANCH_NAME)
      itm.setDisplayName("PR '${ttl}'")
    }
  }
   }
}

    }
  }
}


  @NonCPS
def getItem(branchName) {
  Jenkins.instance.getItemByFullName("multi-docker/${branchName}")
}

@NonCPS
def getTitle(json) {
    def slurper = new groovy.json.JsonSlurper()
    def jsonObject = slurper.parseText(json.content)
    jsonObject.title
}















