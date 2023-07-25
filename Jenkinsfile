pipeline {
    agent { label 'MAVEN_JDK8' }
    triggers { pollSCM('* * * * *') }
    tools {
        jdk 'JDK_8'               
    }
    stages {
        stage('Git') {
            steps {
            git url: 'https://github.com/SyedSohail123/gol-jfrog.git',
                branch: 'master'
            }
        }
        stage('Building Artifacts and pushing to Jfrog Repository') {
            steps {
                export PATH="/usr/lib/jvm/java-8-openjdk-amd64/bin:$PATH"
                sh 'java --version'
                sh 'mvn --version'
                
                // rtMavenDeployer (
                //     tool: 'default'
                //     id: "MAVEN_DEPLOYER",
                //     serverId: "Jfrog_Devops",
                //     releaseRepo: 'qtdevops-libs-release-local',
                //     snapshotRepo: 'qtdevops-libs-snapshot-local'
                // )
                // rtMavenRun (                    
                //     pom: 'pom.xml',
                //     goals: 'clean install',
                //     deployerId: "MAVEN_DEPLOYER"
                // )
                // rtPublishBuildInfo (
                //     serverId: "Jfrog_Devops"
                // )   
            }
        }
        stage('Publishing Test-Results') {
            steps {
            junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
    }
}