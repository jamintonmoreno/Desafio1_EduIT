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
        
        stage('Generated Temporal Password') {
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

                    @Grab(group='javax.mail', module='javax.mail-api', version='1.6.2')
                    @Grab(group='com.sun.mail', module='javax.mail', version='1.6.2')

                    import javax.mail.*
                    import javax.mail.internet.*

                    def enviarCorreo() {
                        // Configura las propiedades para la sesión de correo
                        def props = new Properties()
                        props.setProperty("mail.smtp.host", "smtp.gmail.com")
                        props.setProperty("mail.smtp.port", "587")
                        props.setProperty("mail.smtp.auth", "true")
                        props.setProperty("mail.smtp.starttls.enable", "true")

                        // Crea una autenticación para tu cuenta de Gmail
                        def auth = new Authenticator() {
                            protected PasswordAuthentication getPasswordAuthentication() {
                                return new PasswordAuthentication("tu_correo@gmail.com", "tu_contraseña")
                            }
                        }

                        // Crea una sesión de correo con la autenticación
                        def session = Session.getInstance(props, auth)

                        // Crea un mensaje de correo electrónico
                        def message = new MimeMessage(session)
                        message.setFrom(new InternetAddress("tu_correo@gmail.com"))
                        message.addRecipient(Message.RecipientType.TO, new InternetAddress("destinatario@example.com"))
                        message.setSubject("Asunto del correo")
                        message.setText("Cuerpo del mensaje")

                        // Envía el correo electrónico
                        Transport.send(message)
                    }
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