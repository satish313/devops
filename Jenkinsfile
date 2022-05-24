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
                nexusArtifactUploader artifacts: [[artifactId: '$BUILD_TIMESTAMP', classifier: '', file: 'gameoflife-web/target/gameoflife.war', type: 'war']], credentialsId: '48f6156d-2d85-41e7-b877-d9af7e08da1e', groupId: 'game', nexusUrl: '54.197.4.158:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'game', version: '$BUILD_ID'
                deploy adapters: [tomcat8(credentialsId: '1945b3b4-9c92-436a-b95f-a418918301d7', path: '', url: 'http://23.20.229.133:8080')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
                