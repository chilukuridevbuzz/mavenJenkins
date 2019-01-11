pipeline {
    agent any
    stages {
        stage ('Checkout Code') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/gouthamchilakala/PetClinic.git']]])
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
}
