pipeline {
    agent any
    stages {
        stage ('Checkout Code') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/chilukuridevbuzz/mavenJenkins.git']]])
            }
        }
        stage ( 'Compile') {
            steps {
                sh 'mvn compile'
            }
        }
        stage ( ' Test Cases') {
            steps {
                sh 'mvn test'
            }
        }
        stage ( ' Package' ) {
            steps {
                sh 'mvn package'
            }
        }
    }
   post {
        always {
           // emailext body: 'A Test EMail', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test'
           sh 'zip reports.zip target/surefire-reports/'
            archiveArtifacts artifacts: 'reports.zip', onlyIfSuccessful: true
            echo 'I will always say Hello again!'
    
            emailext attachLog: true, attachmentsPattern: 'reports.zip',
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
                recipientProviders: [developers(), requestor()],
                subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
        }
    }
}
