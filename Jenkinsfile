pipeline {
    agent any
    tools {
       maven "Maven"
    }
    stages {
        stage('Build') {
            steps {
                git 'https://github.com/wakaleo/game-of-life.git'
                sh "mvn -Dmaven.test.failure.ignore=true clean install"
                nexusArtifactUploader artifacts: [[artifactId: '$BUILD_TIMESTAMP', classifier: '', file: 'gameoflife-web/target/gameoflife.war', type: 'war']], credentialsId: '41c64ffa-5325-46b0-b7fa-151f7acc9fc7', groupId: 'satish', nexusUrl: '54.164.140.94:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'game', version: '$BUILD_ID'
                deploy adapters: [tomcat8(credentialsId: '2da716d9-55e8-4cba-8171-61861adcc872', path: '', url: 'http://18.205.18.70:8080')], contextPath: null, war: '**/*.war'
            }
        }
}
}