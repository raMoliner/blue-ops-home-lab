# Docker Basics 

## ¿Qué es Docker?

Docker permite ejecutar aplicaciones como contenedores. Un contenedor es un proceso aislado que corre a partir de una imagen. 

## Imagen vs contenedor 

Una imagen es una plantilla. Contiene la aplicación y sus dependicas.

Un contenedor es una instancia creada desde una imagen. Puede estar corriendo, detenido o eliminado.

Ejemplo: 

'''text 
Imagen: nginx 
Contenedor: blueops-web 

### Comandos básicos

Ver Imágenes

'''
sudo docker images - Muestra las imágenes descargadas localmente. 
'''

Ver contenedores corriendo
'''
sudo docker ps - Muestra solo contenedores activos. 
''' 

Ver todos los contenedores
'''
sudo docker ps -a - Muestra contenedores activos y detenidos. 
'''

Crear y ejecutar un contenedor 
'''
sudo docker run -d --name blueops-web -p 8080:80 nginx - Crea un contenedor llamado "blueops-web" desde la imagen "nginx". 
'''

Detener un contenedor 
'''
sudo docker stop blueops-web - Detiene el proceso del contenedor llamado "blueops-web".
'''

Iniciar un contenedor detenido
'''
sudo docker start blueops-web - Vuelve a iniciar un contenedor existente. 
'''

Ver logs
'''
sudo docker logs blueops-web - Muestra evidencia de ejecución y accesos del servicio. 
''' 

Eliminar un contenedor
'''
sudo docker rm blueops-web - Elimina el contenedor pero no elimina la imagen. 
'''
