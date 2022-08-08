pipeline {
    agent any
    environment {
        projectName = 'Cleaning The Workspace'
    }
    stages {
        stage('Checkout repository') {
            steps {
                // You can choose to clean workspace before build as follows
                cleanWs()
                checkout scm
            }
        }
        stage ('Build Application') {
            steps {
              sh 'npm i'
              sh 'npm run build'
            }
        }

//Other steps can be added here

        stage("Deploy Application"){
            steps{
                sh "kubectl apply -f deployment.yaml"
              //Then clean the workspace after deployment ignoring node_modules directory
                cleanWs deleteDirs: true, patterns: [[pattern: 'node_modules', type: 'EXCLUDE']]
            }
        }
