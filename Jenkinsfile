pipeline {
    agent any
	tools {
        maven "MAVEN3"
        jdk "OracleJDK8"
    }

    environment {
        SNAP_REPO = "vprofile-snapshot"
        NEXUS_USER = "admin"
        NEXUS_PASS = "admin"
        NEXUSIP = "172.31.34.249"
        NEXUSPORT = "8081"
        RELEASE_REPO = "vprofile-release"
	    NEXUS_GRP_REPO = "vpro-maven-group"
        NEXUS_LOGIN = "nexuslogin"
        CENTRAL_REPO = "vpro-maven-central"
    }
	
    stages{
        stage('Build'){
            steps {
                sh 'mvn -s settings.xml install -DskipTests'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('UNIT TEST'){
            steps {
                sh 'mvn test'
            }
        }
        stage ('CODE ANALYSIS WITH CHECKSTYLE'){
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
        }
    }
}
