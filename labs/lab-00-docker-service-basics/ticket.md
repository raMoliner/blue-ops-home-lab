# Ticket — Lab 00 Docker Service Basics

## Resumen

Se ejecutó una simulación controlada de disponibilidad, caída y recuperación de un servicio web local ejecutado en Docker.

El servicio utilizado fue Nginx, publicado desde el puerto `80` interno del contenedor hacia el puerto `8080` del host Fedora.

## Clasificación

* Tipo de evento: Disponibilidad
* Área: NOC / Infraestructura
* Severidad simulada: Media
* Estado: Cerrado
* Entorno: Laboratorio local

## Activo afectado

* Host: Fedora local
* Contenedor: `blueops-web`
* Imagen: `nginx`
* Puerto publicado: `8080:80`
* URL validada: `http://localhost:8080`

## Estado inicial

Se validó que no existían contenedores corriendo antes de iniciar el laboratorio.

Luego se creó el contenedor:

```bash
sudo docker run -d --name blueops-web -p 8080:80 nginx
```

El contenedor quedó en estado `Up` y con el puerto publicado correctamente:

```text
0.0.0.0:8080->80/tcp
```

## Validación de disponibilidad

Se validó el servicio mediante:

```bash
curl -I http://localhost:8080
```

Resultado observado:

```text
HTTP/1.1 200 OK
Server: nginx/1.31.3
```

Interpretación:

El servicio web estaba disponible y respondiendo correctamente por HTTP.

## Evidencia de tráfico

Se generó tráfico HTTP hacia el servicio:

```bash
curl http://localhost:8080
curl -I http://localhost:8080
```

Luego se revisaron logs:

```bash
sudo docker logs blueops-web
```

Eventos observados:

```text
"HEAD / HTTP/1.1" 200
"GET / HTTP/1.1" 200
```

Interpretación:

El servicio recibió solicitudes HTTP exitosas desde `curl`.

## Simulación de caída

Se detuvo el servicio con:

```bash
sudo docker stop blueops-web
```

Después de detener el contenedor, `docker ps` no mostró contenedores activos.

Se confirmó el impacto con:

```bash
curl -I http://localhost:8080
```

Resultado esperado/observado:

```text
curl: (7) Failed to connect to localhost port 8080
```

Interpretación:

El servicio dejó de responder desde la perspectiva del cliente.

## Estado del contenedor detenido

Se validó con:

```bash
sudo docker ps -a
```

Resultado observado:

```text
blueops-web   Exited (0)
```

Interpretación:

El contenedor seguía existiendo, pero estaba detenido. El código `Exited (0)` indica que el proceso terminó correctamente.

## Recuperación

Se recuperó el servicio con:

```bash
sudo docker start blueops-web
```

Luego se validó nuevamente:

```bash
sudo docker ps
curl -I http://localhost:8080
```

Resultado:

```text
HTTP/1.1 200 OK
```

Interpretación:

El servicio fue recuperado correctamente y volvió a estar disponible por HTTP.

## Causa raíz

La indisponibilidad fue causada por una detención manual controlada del contenedor durante el laboratorio.

## Acción realizada

* Se levantó un servicio Nginx en Docker.
* Se validó disponibilidad HTTP.
* Se generó tráfico.
* Se revisaron logs.
* Se simuló una caída.
* Se confirmó impacto desde cliente.
* Se recuperó el servicio.
* Se validó recuperación.
* Se documentó evidencia.

## Lección aprendida

Un servicio debe validarse desde varias perspectivas:

1. Estado del contenedor.
2. Puerto publicado.
3. Respuesta HTTP.
4. Logs.
5. Impacto tras caída.
6. Confirmación de recuperación.

Este flujo representa una tarea básica de monitoreo NOC: validar, investigar, confirmar impacto, recuperar y documentar.
