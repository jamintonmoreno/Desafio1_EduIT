# Desafio1_EduIT
Este es el primer desafío del Bootcamp Devops Engineer. Este proyecto tiene como objetivo crear usuarios en un sistema Ubuntu mediante el uso de un pipeline declarativo ejecutado por Jenkins, donde el script esta guardado en un repositorio de GitHub.

Estos son los requisitos previos que debe tener para ejecutar este proyecto;
1. Contar con un sistema Linux (Preferiblemente Ubuntu). Puede usar una VM (Máquina virtual) con un sistema Ubuntu.
2. Tener instalado Jenkins en su máquina.
3. Tener una cuenta de GitHub.

Para ejecutar el proyecto siga los siguientes pasos;
1. Inicie sesión en su sistema Linux.
2. Inicie sesión en Jenkins.
3. Inicie sesion en GitHud. Clone el repositorio usando el siguiente link https://github.com/jamintonmoreno/Desafio1_EduIT.git
4. Solicite su "Access Token" de GitHub, en caso que cree un repositorio "PRIVADO".
5. Al ingresar a Jenkins vaya al "Panel de Control > Administrar Jenkins > Credential > System > Add Credential.
   En la opcion "Username" escriba su usuario de github. En la opcion "Password" use el "Access Token" que se suministro github.
   Luego dar clic en "Save". Esa credential la va necesitar luego. Regrese al "Panel de control".
   
![image](https://github.com/jamintonmoreno/Desafio1_EduIT/assets/74082502/53953c3e-3ba0-4e58-bd99-b6d86fd095de)

8. Estando en la interfaz de usuario de Jenkins, seleccione "Nueva Tarea"
   
   ![image](https://github.com/jamintonmoreno/Desafio1_EduIT/assets/74082502/1abaf104-d11b-43b6-808a-361ed9fa49bf)

   
10. Asigne el nombre que desea a la tarea. Seleccione la opción "Pipeline" luego haga clic en "Ok".
   ![image](https://github.com/jamintonmoreno/Desafio1_EduIT/assets/74082502/e2276bd9-731d-400e-a358-e0c7114d67e5)

11. Vaya a la sección "Pipeline" en la opcion "Definition" seleccione "Pipeline script from SCM". Se desplegara un menu, en la opcion "SCM" seleccion "Git".
12. Se desplegara un formulario, en la opcion "Repository URL" ingrese el link de su repositorio de github. Y en la opcion "Credential" seleccione la credencial creada
    con anterioridad. Y haga clic en "Guardar".
    ![image](https://github.com/jamintonmoreno/Desafio1_EduIT/assets/74082502/b3409cf9-835e-4652-8f6d-29016aa0986f)

13. Cuando este en la Dashboard del job. De click en "Build Now o Construir Ahora". Esto ejecutará el job y en la parte inferior izquierda de la pantalla se habilidatara una sección donde permitira ver la información de ejecución. Dando clic en "Console Output" podra ver al detalle los registros de la ejecución.
    ![image](https://github.com/jamintonmoreno/Desafio1_EduIT/assets/74082502/6f6c8097-a67d-42c0-9dcd-569283559bfd)


 
