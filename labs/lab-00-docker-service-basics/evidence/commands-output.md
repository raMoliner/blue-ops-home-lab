# Lab 00 — Commands Output

## Fecha
jue 23 jul 2026 12:01:29 -04

## Estado inicial de Docker
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

## Crear contenedor Nginx
6e3f1a2c9237815a6fcc79b3788bca0f0bbb60bda65828c8b514ed9d72886c9c

## Validar contenedor corriendo
CONTAINER ID   IMAGE     COMMAND                  CREATED                  STATUS                  PORTS                                     NAMES
6e3f1a2c9237   nginx     "/docker-entrypoint.…"   Less than a second ago   Up Less than a second   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   blueops-web

## Validar HTTP headers
HTTP/1.1 200 OK
Server: nginx/1.31.3
Date: Thu, 23 Jul 2026 16:01:30 GMT
Content-Type: text/html
Content-Length: 896
Last-Modified: Wed, 15 Jul 2026 16:03:14 GMT
Connection: keep-alive
ETag: "6a57af42-380"
Accept-Ranges: bytes


## Generar tráfico HTTP completo
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>

## Revisar logs
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
172.17.0.1 - - [23/Jul/2026:16:01:30 +0000] "HEAD / HTTP/1.1" 200 0 "-" "curl/8.18.0" "-"
172.17.0.1 - - [23/Jul/2026:16:01:30 +0000] "GET / HTTP/1.1" 200 896 "-" "curl/8.18.0" "-"

## Simular caída
blueops-web

## Confirmar contenedores activos después de caída
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

## Confirmar impacto HTTP después de caída

## Ver contenedor detenido
CONTAINER ID   IMAGE     COMMAND                  CREATED        STATUS                              PORTS     NAMES
6e3f1a2c9237   nginx     "/docker-entrypoint.…"   1 second ago   Exited (0) Less than a second ago             blueops-web

## Recuperar servicio
blueops-web

## Validar recuperación
CONTAINER ID   IMAGE     COMMAND                  CREATED        STATUS                  PORTS                                     NAMES
6e3f1a2c9237   nginx     "/docker-entrypoint.…"   1 second ago   Up Less than a second   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   blueops-web
HTTP/1.1 200 OK
Server: nginx/1.31.3
Date: Thu, 23 Jul 2026 16:01:31 GMT
Content-Type: text/html
Content-Length: 896
Last-Modified: Wed, 15 Jul 2026 16:03:14 GMT
Connection: keep-alive
ETag: "6a57af42-380"
Accept-Ranges: bytes



## Revalidación de caída capturando stderr

### Detener servicio
blueops-web

### Validar impacto HTTP con stderr capturado
  % Total    % Received % Xferd  Average Speed  Time    Time    Time   Current
                                 Dload  Upload  Total   Spent   Left   Speed
  0      0   0      0   0      0      0      0                              0
curl: (7) Failed to connect to localhost port 8080 after 0 ms: Could not connect to server

### Recuperar servicio
blueops-web

### Validar recuperación
  % Total    % Received % Xferd  Average Speed  Time    Time    Time   Current
                                 Dload  Upload  Total   Spent   Left   Speed
  0      0   0      0   0      0      0      0                              0
curl: (56) Recv failure: Conexión reinicializada por la máquina remota
