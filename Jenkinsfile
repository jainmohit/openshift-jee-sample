try {
   timeout(time: 20, unit: 'MINUTES') {
      node('maven') {
          //stage('build') {
          //  git url: "https://github.com/danmcp/openshift-jee-sample.git"
          // openshiftBuild(buildConfig: 'somethingcool', showBuildLogs: 'true')
          //}
          stage('test') {
            git url: "https://github.com/danmcp/openshift-jee-sample.git"
            sh 'mvn clean'
          }
          stage('approval') {
            input "Approve?"
          }
          stage('deploy') {
            openshiftDeploy(deploymentConfig: 'somethingcool')
          }
          stage('scale') {
            openshiftScale(deploymentConfig: 'somethingcool', replicaCount: '2')
          }
          stage('system test') {
            sh "curl http://somethingcool:8080 | grep WildFly"
          }
        }
   }
} catch (err) {
   echo "in catch block"
   echo "Caught: ${err}"
   currentBuild.result = 'FAILURE'
   throw err
}
