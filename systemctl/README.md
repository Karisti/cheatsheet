# Servicios en Ubuntu con Systemd

## Index<!-- omit in toc -->
- [Conceptos básicos](#conceptos-básicos)
  - [¿Qué es un servicio?](#qué-es-un-servicio)
  - [Cómo se gestionan los servicios o demonios en GNU Linux](#cómo-se-gestionan-los-servicios-o-demonios-en-gnu-linux)
- [Usando Systemd](#usando-systemd)
  - [Comandos habituales](#comandos-habituales)
  - [Iniciar nuevo servicio](#iniciar-nuevo-servicio)
  - [Quitar un servicio](#quitar-un-servicio)
  - [Algunos comandos útiles](#algunos-comandos-útiles)
  - [Bibliografía](#bibliografía)
  

## Conceptos básicos

### ¿Qué es un servicio?
Un servicio es un programa que se ejecuta, o está esperando ser ejecutado, en segundo plano.

Los servicios o procesos tienen las siguientes características:
- No acostumbran a tener una interfaz gráfica para que los usuarios puedan interactuar de forma directa con ellos.
- Los servicios o demonios normalmente son inicializados con el arranque del sistema.
- Normalmente están a la espera de que pase un evento para a posteriori poder realizar su función.
- Toda la actividad que generan los servicios queda registrada en los logs del sistema mediante syslog y/o journalctl.

<div align="right">
  <small><a href="#servicios-en-ubuntu-con-systemd">🡡 Vuelta al Index</a></small>
</div>

### Cómo se gestionan los servicios o demonios en GNU Linux
Los servicios o demonios se gestionan mediante los demonios Init o Systemd.

El primer servicio que inicia el Kernel de Linux es Init o Systemd. Seguidamente, init o systemd son los encargados de cargar el resto de servicios del sistema operativo. Por lo tanto Init o Systemd son los padres de todos los demonios o servicios que se inicializan en nuestro sistema operativo.

Init y Systemd siempre están activos hasta que el sistema se apaga. Mientras estos servicios estén activos los podremos usar para gestionar los servicios que se inician y paran en nuestro ordenador o servidor.

En el caso que systemd o init no se inicien, nuestro ordenador nunca podrá llegar a arrancar. Por lo tanto son demonios extremadamente importantes.

<div align="right">
  <small><a href="#servicios-en-ubuntu-con-systemd">🡡 Vuelta al Index</a></small>
</div>

## Usando Systemd

### Comandos habituales
- `sudo systemctl start {nombre_servicio.service}` para iniciar el servicio.
- `sudo systemctl status {nombre_servicio.service}` para comprobar el estado del servicio.
- `sudo systemctl restart {nombre_servicio.service}` para reiniciar el servicio.
- `sudo systemctl stop {nombre_servicio.service}` para parar el servicio.
- `sudo systemctl reload {nombre_servicio.service}` para recargar la configuración del servicio sin reiniciarlo ni pararlo en ningún momento.
- `sudo systemctl enable {nombre_servicio.service}` para habilitarlo. Necesario para que un servicio arranque de forma automática al iniciar el ordenador.
- `sudo systemctl disable {nombre_servicio.service}` si queremos que al arrancar el ordenador no se cargue el servicio.
- `sudo systemctl mask {nombre_servicio.service}` si además de deshabilitarlo queremos que no se pueda iniciar manualmente ni automáticamente después de iniciar la sesión podemos enmascararlo.
- `sudo systemctl unmask {nombre_servicio.service}` si queremos desenmascarar el servicio que acabamos enmascarar para que se pueda iniciar manualmente o automáticamente después de iniciar la sesión.

<div align="right">
  <small><a href="#servicios-en-ubuntu-con-systemd">🡡 Vuelta al Index</a></small>
</div>

### Iniciar nuevo servicio
Los archivos de los servicios se guardan en "/etc/systemd/system/".

#### Creamos el archivo del servicio y escribimos en él
```
sudo touch /etc/systemd/system/{nombre_servicio}.service
sudo chmod 664 /etc/systemd/system/{nombre_servicio}.service
sudo vim /etc/systemd/system/{nombre_servicio}.service
```
#### Escribimos la configuración del servicio, ejemplo
```
[Unit]
Description=Servicio que obtiene todos los siniestros de bomberos cada minuto

[Service]
Type=simple
EnvironmentFile=/home/ubuntu/dev/backend/.env
ExecStart=/usr/bin/python3 /home/ubuntu/dev/backend/operador/bomberos/main.py

ExecStop=/usr/bin/python3 /home/ubuntu/dev/backend/services.py operador_bomberos inactive

SuccessExitStatus=143
TimeoutStopSec=10
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```
#### Indicamos al sistema que hay un nuevo servicio
```
sudo systemctl daemon-reload
```
#### Iniciamos el servicio y lo habilitamos para que se inicie automáticamente al arranque
```
sudo systemctl start name.service
sudo systemctl enable name.service
```

<div align="right">
  <small><a href="#servicios-en-ubuntu-con-systemd">🡡 Vuelta al Index</a></small>
</div>

### Quitar un servicio
#### Paramos y deshabilitamos el servicio
```
systemctl stop {nombre_servicio}.service
systemctl disable {nombre_servicio}.service
```
#### Eliminamos el servicio
```
sudo rm /etc/systemd/system/{nombre_servicio}.service
sudo rm /etc/systemd/system/{nombre_servicio}.service symlinks that might be related
```
#### Indicamos al sistema que hemos borrado el servicio
```
systemctl daemon-reload
systemctl reset-failed
```

<div align="right">
  <small><a href="#servicios-en-ubuntu-con-systemd">🡡 Vuelta al Index</a></small>
</div>

### Algunos comandos útiles
- `systemctl help {nombre_servicio.service}` para obtener ayuda del servicio {nombre_servicio.service}.
- `systemctl list-dependencies {nombre_servicio.service}` para conocer la totalidad de dependencias que {nombre_servicio.service} necesita para realizar su función.
- `systemctl list-dependencies --before {nombre_servicio.service}` para conocer los servicios que se usaran después de ejecutar {nombre_servicio.service}.
- `systemctl list-dependencies --after {nombre_servicio.service}` para conocer los servicios y unidades que tienen que estar activos antes de iniciar {nombre_servicio.service}.

<div align="right">
  <small><a href="#servicios-en-ubuntu-con-systemd">🡡 Vuelta al Index</a></small>
</div>

### Bibliografía
- [Documentación Red Hat](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system_administrators_guide/sect-managing_services_with_systemd-unit_files)
- [https://geekland.eu/systemctl-administrar-servicios-linux/](https://geekland.eu/systemctl-administrar-servicios-linux/)

<div align="right">
  <small><a href="#servicios-en-ubuntu-con-systemd">🡡 Vuelta al Index</a></small>
</div>
