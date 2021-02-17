pipeline{
    environment{
	JAVA_TOOL_OPTIONS="-Duser.home=/var/maven"
    }
    agent{
        docker{
            image 'maven:3.6.0-jdk-13'
            label 'docker-remote-agent'
            args '-v /home/osboxes/maven:/var/maven/.m2 -e MAVEN_CONFIG=/var/maven/.m2'
        }
    }
    options{
        buildDiscarder(logRotator(numToKeepStr: '2'))
        disableConcurrentBuilds()
        disableResume()
        timestamps()
    }
    stages{
        stage('check content'){
            steps{
                sh 'pwd'
                sh 'ls -ltr'
            }
        }
        stage('Build'){
            steps{
                sh 'mvn --version'
                sh 'mvn clean package'
            }
        }
    }
    post{
        always{
            archiveArtifacts artifacts: 'target/*.war', fingerprint: true, allowEmptyArchive: false, onlyIfSuccessful: false;
        }
        cleanup{
            cleanWs()
        }
    }
}
