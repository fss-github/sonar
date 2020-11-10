#!/usr/bin/groovy

node("master"){
    //checkout
    checkout([$class: 'GitSCM',
             branches: [[name: '*/master']], 
             doGenerateSubmoduleConfigurations: false, 
             extensions: [], submoduleCfg: [], 
             userRemoteConfigs: [[credentialsId: 'dc85759a-1cc0-461e-8ba9-383e3169e5f3', 
             url: 'http://gitlab.kgc.cn/kgc/kgcweb.git']]])
    //Build
    sh "mvn ${buildShell}"
    
    //Sonar
    sh  """
        sonar-scanner -Dsonar.projectKey=${serviceName} \
                      -Dsonar.projectName=${serviceName} \
                      -Dsonar.login=765062f69357d1b970e7dfb1b87da77ef2aa7407 \
                      -Dsonar.sources=src \
                      -Dsonar.host.url=${sonarServer}
        """
}
