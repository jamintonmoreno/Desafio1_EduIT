pipeline {
    agent any
    
    stages {
        stage('Solicitar Datos de Entrada') {
            steps {
                script {
                    def userInput = input(
                        id: 'userInput', message: 'Ingrese los datos del usuario:',
                        parameters: [
                            string(defaultValue: '', description: 'Login (nombre.apellido):', name: 'login'),
                            string(defaultValue: '', description: 'Nombre y Apellido:', name: 'nombreApellido'),
                            choice(choices: ['Contabilidad', 'Finanzas', 'Tecnología'], description: 'Departamento:', name: 'departamento')
                        ]
                    )
                    
                    def login = userInput['login']
                    def nombreApellido = userInput['nombreApellido']
                    def departamento = userInput['departamento']
                }
            }
        }
        
        stage('Generar Contraseña Temporal') {
            steps {
                script {
                    def password = sh(script: "openssl rand -base64 12 | tr -d '='", returnStdout: true).trim()
                    // Podrías almacenar esta contraseña temporal en un archivo o variable para usarla posteriormente
                }
            }
        }
        
        stage('Crear Usuario en Linux') {
            steps {
                script {
                    sh "sudo useradd -m -s /bin/bash -G ${departamento} ${login}"
                    sh "echo ${login}:${password} | sudo chpasswd"
                }
            }
        }
        
        stage('Enviar Contraseña por Correo Electrónico') {
            steps {
                script {
                    // Aquí deberías tener una lógica para enviar un correo electrónico al usuario con su contraseña temporal
                    // Por ejemplo, utilizando la API de un proveedor de correo electrónico o un servidor SMTP
                }
            }
        }
    }
    
    post {
        success {
            echo 'El usuario ha sido creado exitosamente.'
        }
        failure {
            echo 'Ha ocurrido un error durante la creación del usuario.'
        }
    }
}