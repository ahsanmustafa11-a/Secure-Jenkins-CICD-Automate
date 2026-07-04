@Library('shared') _

pipeline {

    agent { label 'dev-agent-key' }

    stages {

        stage('Clone') {
            steps {
                script {
                    clone("https://github.com/ahsanmustafa11-a/Secure-Jenkins-CICD-Automate.git", "main")
                }
            }
        }

        stage('SonarQube') {
            steps {
                script {
                    sonarcube()
                }
            }
        }

        stage('OWASP Dependency Check') {
            steps {
                script {
                    owasp()
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker compose build'
            }
        }

        stage('Trivy') {
            steps {
                script {
                    trivy()
                }
            }
        }

        stage('Docker Registry') {
            steps {
                script {
                    dockerRegistry()
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    dockerDeploy()
                }
            }
        }

        stage('OWASP ZAP') {
            steps {
                script {
                    owaspZap(APP_URL)
                }
            }
        }

    }

    post {

        always {

            script {

                notify(
                    "ahsan820820@gmail.com",
                    currentBuild.currentResult
                )

            }

        }

    }

}
