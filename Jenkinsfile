pipeline {
    agent any

    parameters {
        string(name: 'Login', description: 'Please enter your username', defaultValue: '')
        string(name: 'FirstLastName', description: 'Please enter your First and Last Name', defaultValue: '')
        choice(name: 'Departament', choices: ['Accounting', 'Finance', 'Technology'], description: 'Choose department to which you belong')
    }

    stages {
        stage('Create user') {
            steps {
                sh "sudo useradd -m -s /bin/bash -c '${FirstLastName}' ${Login}"
            }
        }

        stage('Generate temporal password') {
            steps {
                script {
                    def passwordTemporal = sh(script: 'sudo openssl rand -base64 10', returnStdout: true).trim()
                    echo "Your password is: ${passwordTemporal}"
                    env.PASSWORD_TEMPORAL = passwordTemporal
                }
            }
        }

        stage('Assign temporary password') {
            steps {
                sh "echo ${Login}: ${PASSWORD_TEMPORAL} | sudo chpasswd"
            }
        }
    }
}