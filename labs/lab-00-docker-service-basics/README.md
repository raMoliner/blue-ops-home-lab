#Lab 00 - Docker Service Basics# Lab 00 — Docker Service Basics

## Objetivo

Simular una tarea básica de operación NOC/Infraestructura usando Docker y Nginx.

El laboratorio consiste en levantar un servicio web local, validar disponibilidad HTTP, revisar logs, simular una caída, confirmar impacto, recuperar el servicio y documentar evidencia.

## Rol simulado

Analista NOC Junior / Analista de Monitoreo / Soporte de Infraestructura Junior.

## Escenario

Un servicio web local debe estar disponible en el puerto `8080` del host Fedora. El servicio corre dentro de un contenedor Docker basado en la imagen `nginx`.

Como analista, debo validar:

* Si el contenedor está corriendo.
* Si el puerto está publicado.
* Si el servicio responde HTTP.
* Si existen logs de acceso.
* Qué ocurre cuando el servicio cae.
* Cómo recuperar el servicio.
* Cómo documentar evidencia.

## Conceptos practicados

* Imagen Docker.
* Contenedor Docker.
* Contenedor corriendo vs detenido.
* Publicación de puertos.
* Validación HTTP con `curl`.
* Logs de contenedor.
* Simulación de caída.
* Recuperación de servicio.
* Evidencia operacional.

## Arquitectura simple

```text
Fedora host
   |
   | Puerto 8080
   v
Docker container: blueops-web
   |
   | Puerto 80 interno
   v
Nginx
```

## Comandos usados

### Ver contenedores activos

```bash
sudo docker ps
```

Uso este comando para validar qué contenedores están corriendo en este momento.

### Ver todos los contenedores

```bash
sudo docker ps -a
```

Uso este comando para ver contenedores activos y detenidos.

### Crear servicio web

```bash
sudo docker run -d --name blueops-web -p 8080:80 nginx
```

Este comando crea un contenedor llamado `blueops-web` usando la imagen `nginx`.

El parámetro `-p 8080:80` publica el puerto `80` interno del contenedor como puerto `8080` en Fedora.

### Validar disponibilidad HTTP

```bash
curl -I http://localhost:8080
```

Uso `curl -I` para validar cabeceras HTTP sin descargar el contenido completo.

Un resultado `HTTP/1.1 200 OK` indica que el servicio responde correctamente.

### Ver contenido completo

```bash
curl http://localhost:8080
```

Uso este comando para confirmar que el servicio entrega contenido HTML.

### Revisar logs

```bash
sudo docker logs blueops-web
```

Uso este comando para revisar evidencia de arranque del servicio y solicitudes HTTP recibidas.

### Simular caída

```bash
sudo docker stop blueops-web
```

Este comando detiene el contenedor y simula que el servicio web deja de estar disponible.

### Confirmar caída

```bash
curl -I http://localhost:8080
```

Si el servicio está caído, espero un error de conexión.

### Recuperar servicio

```bash
sudo docker start blueops-web
```

Este comando inicia nuevamente el contenedor detenido.

### Confirmar recuperación

```bash
curl -I http://localhost:8080
```

Espero volver a recibir `HTTP/1.1 200 OK`.

## Criterio de éxito

El laboratorio se considera exitoso si se demuestra:

* El contenedor `blueops-web` corre correctamente.
* El puerto `8080` del host apunta al puerto `80` del contenedor.
* El servicio responde con `HTTP/1.1 200 OK`.
* Los logs muestran solicitudes HTTP.
* Al detener el contenedor, el servicio deja de responder.
* Al iniciar el contenedor, el servicio vuelve a responder.
* La evidencia queda documentada.

## Aprendizaje operativo

Un servicio no se valida solo mirando si el proceso existe. Debo confirmar el estado desde varias perspectivas:

1. Estado del contenedor.
2. Puerto publicado.
3. Respuesta HTTP.
4. Logs.
5. Impacto al detener el servicio.
6. Confirmación después de recuperar.

## Explicación de 60 segundos

En este laboratorio levanté un servicio web Nginx dentro de Docker para practicar una tarea básica de operación. Validé que el contenedor estuviera corriendo con `docker ps`, confirmé que el puerto `8080` del host estaba publicado hacia el puerto `80` del contenedor y probé disponibilidad con `curl -I`. Luego revisé logs con `docker logs`, simulé una caída usando `docker stop`, confirmé que el servicio dejó de responder y lo recuperé con `docker start`. Esto representa un flujo básico NOC: validar, revisar evidencia, confirmar impacto, recuperar y documentar.


##Objetivo

Simular una tarea básica de operación NOC/Infraestructura usando Docker y Nginx. 

El laboratorio consiste en levantar un servicio web local, validar disponibilidad HTTP, revisar logs, simular una caída, confirmar impacto, recuperar el servicio y documentar evidencia. 

##Rol simulado 

Analista NOC Junior / Analista de Monitoreo / Soporte de Infraestructura Junior. 

##Escenario 

Un servicio web local debe estar disponible en el puerto 8080 del host Fedora. 

