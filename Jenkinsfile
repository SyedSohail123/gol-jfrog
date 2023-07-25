pipeline {
    agent { label 'MAVEN_JDK8' }
    triggers { pollSCM('* * * * *') }
    tools {
        jdk 'JDK_8'        
    }
    stages {
        stage('Git') {
            git url: 'https://github.com/SyedSohail123/gol-jfrog.git'
                branch: 'declarative'
        }
        stage('Building Artifacts and pushing to Jfrog Repository') {
            steps {
                rtMavenDeployer (
                    id: "MAVEN_DEPLOYER",
                    serverId: "ARTIFACTORY_SERVER",
                    releaseRepo: ARTIFACTORY_LOCAL_RELEASE_REPO,
                    snapshotRepo: ARTIFACTORY_LOCAL_SNAPSHOT_REPO
                )
                rtMavenRun (                    
                    pom: 'pom.xml',
                    goals: 'clean install',
                    deployerId: "MAVEN_DEPLOYER"
                )
                rtPublishBuildInfo (
                    serverId: "ARTIFACTORY_SERVER"
                )   
            }
        }
        stage('Publishing Test-Results') {
            steps {
            junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
    }
}