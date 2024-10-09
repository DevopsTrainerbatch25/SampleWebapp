pipeline{
    agent any
    tools{
        maven 'MAVEN_HOME'
    }
    stages{
        stage('git checkout'){
            steps{
                checkout scmGit(branches: [[name: 'main']], extensions: [], userRemoteConfigs: [[credentialsId: '83fc3807-f1e6-4f39-b0c8-776354d319c4', url: 'https://github.com/DevopsTrainerbatch25/SampleWebapp.git']])
            }
        }
        stage('Build'){
            steps{
                sh 'mvn package -f pom.xml'
            }
        }
        stage('Upload to Nexus'){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'Hsbcib', classifier: '', file: 'target/PollSCM-Hsbcib.war', type: 'war']], credentialsId: '86d45777-94b4-4ae7-8a2e-6a5ff427089c', groupId: 'com.wipro.HSBC', nexusUrl: '34.170.119.196:8081/', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '1.0-SNAPSHOT'
            }
        }
        stage('Deploy to tomcat'){
            steps{
                deploy adapters: [tomcat9(credentialsId: '410d420c-a999-4633-b423-1ca96e04d196', path: '', url: 'http://35.222.226.148:8090/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
