# AYGO-tutorial

 Arquitectura de la aplicación subida a este repositorio:

![image](https://github.com/user-attachments/assets/f79dfe65-86d1-4d94-a859-86c7faa8ff7f)


El código disponible en este repositorio, consiste en una aplicación básica en java usando nextbean versión 23, que se forma por medio de 2 clases:

HelloRestController: Esta clase tiene como función el manejo de peticiones tipo get, realizadas sobre el servicio expuesto (localhost o URL) al correr la aplicación, la petición que se debe realizar es /greeting y la salida esperada es HELLOW WORLD.

RestServiceApplication:Esta es la clase principal, cuya función es validar el valor definido para la variable port, si esta variable no es definida por defecto se asigna el valor 33025, si se ingresa un valor para la variable port, esta es transformada en entero y se asigna el valor a port, el valor de port corresponde al puerto por donde va a estar expuesta la aplicación.

En el archivo pom están contenidas las dependencias que requiere mavens y un plugin para copiar estas dependencias en un directorio aparte para poder exportarlo a Docker, donde no se cuenta con mavens, es importante mencionar que en las propiedades se indica que la versión es 23, si se usa otra versión de NetBeans, se debe cambiar ese valor.

para poder correr la aplicación se debe hacer un build del proyecto para verificar que no halla errores y las dependencias sean copiadas en el directorio, una vez halla compilado se debe ejecutar la siguiente linea de comandos por CMD en la ruta donde se encuentra el proyecto.

java -cp "target/classes;target/dependency/*" com.mycompany.tutorial3.RestServiceApplication

En el caso de usar Linux en lugar del ; que esta después de /clases se debe usar :

La salida del comando debe indicar que hay un proceso corriendo y desde un navegador ingresando a la siguiente URL y ejecutando la petición get /greeting, se debe obtener la salida esperada (HELLOW WORLD)

http://localhost:33025/greeting

en caso de que se defina un valor para port, se debe cambiar ese valor por el 33025 del paso anterior.


Adicionalmente en el repositorio también se encuentra con un archivo de dockerfile para poder generar una imagen de Docker, en el dockerfile se indica la versión 23 de NetBeans, en caso de usar otra versión este valor se debe cambiar, también se indica que la aplicación corre por el puerto 33025 y que se deben copiar las dependencias que se exportaron al directorio al momento de compilar el código en los pasos anteriores.

Para crear la imagen de Docker se debe acceder por cmd a la ruta donde se encuentra el proyecto y ejecutar el siguiente comando:

docker build --tag "nombre de la imagen a crear" .

el . en el comando indica que el archivo dockerfile se encuentra en esa misma ruta, una vez la imagen ah sido creada, se debe exponer el servicio por medio de un container que tenga como base la imagen creada en Docker en el paso anterior, por medio del siguiente comando:

docker run -d -p "puerto por el que se va a acceder":33025 --name "nombre del container" "nombre de la imagen en docker"

Para poder probar que la aplicación esta funcionando correctamente desde Docker, el container debe estar corriendo y se debe acceder a la siguiente URL y ejecutar la petición get /greeting

http://localhost:"puerto configurado al crear el container"/greeting

Si todo esta correcto, se debe mostrar la salida de la petición get esperada, HELLOW WORLD

La imagen que se crea en Docker, se puede subir a dockerhub,para que esta este disponible y se pueda desplegar en otros ambientes que cuenten con Docker, como una maquina virtual montada en alguna nube, como AWS, AZURE u otros.





