pipeline {
    agent any

    parameters {
        string(name: 'Login', description: 'Por favor ingrese su nombre de usuario', defaultValue: '')
        string(name: 'NombreApellido', description: 'Ingrese su Nombre y Apellido', defaultValue: '')
        choice(name: 'Departamento', choices: ['Contabilidad', 'Finanzas', 'Tecnología'], description: 'Escoja Departamento al que pertenece')
    }

    stages {
        stage('Crear usuario') {
            steps {
                sh "sudo useradd -m -s /bin/bash -c '${NombreApellido}' ${Login}"
            }
        }

        stage('Generar password temporal') {
            steps {
                script {
                    def passwordTemporal = sh(script: 'sudo openssl rand -base64 10', returnStdout: true).trim()
                    echo "Su contraseña es: ${passwordTemporal}"
                    env.PASSWORD_TEMPORAL = passwordTemporal
                }
            }
        }

        stage('Asignar contraseña temporal') {
            steps {
                sh "echo ${Login}: ${PASSWORD_TEMPORAL} | sudo chpasswd"
            }
        }
    }
}