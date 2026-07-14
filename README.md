# Laboratorio Ansible con Docker

## Objetivo de la práctica

Crear un laboratorio con dos servidores Linux utilizando Docker y administrarlos mediante Ansible.  
En esta práctica se configuraron dos contenedores Ubuntu 24.04 y se automatizaron tareas mediante un playbook de Ansible.

## Estructura del proyecto

```
ansible-lab/
├── docker-compose.yml
├── inventory.ini
├── playbook.yml
└── README.md
```

## Creación de los servidores Docker

Se crearon dos servidores Linux utilizando Docker Compose:

- server1
- server2

Los servidores utilizan la imagen:

```
ubuntu:24.04
```

Para iniciar los contenedores se utilizó el comando:

```bash
docker compose up -d
```

Para verificar que los contenedores están ejecutándose:

```bash
docker ps
```

## Configuración de Ansible

Se creó el archivo `inventory.ini` para definir los servidores administrados:

```ini
[docker]
server1 ansible_connection=docker
server2 ansible_connection=docker
```

Para comprobar la conexión entre Ansible y los servidores se ejecutó:

```bash
ansible docker -i inventory.ini -m ping
```

## Playbook de Ansible

El archivo `playbook.yml` realiza las siguientes tareas en ambos servidores:

- Mostrar el nombre del host.
- Mostrar el sistema operativo.
- Crear el directorio `/tmp/ansible-demo`.
- Crear el archivo `info.txt`.
- Escribir en el archivo información del servidor y del sistema operativo.
- Crear mediante un loop los directorios:
  - logs
  - backup
  - config
- Mostrar un mensaje únicamente cuando el sistema operativo sea Ubuntu.

## Ejecución del Playbook

Para ejecutar el playbook se utilizó el comando:

```bash
ansible-playbook -i inventory.ini playbook.yml
```

## Resultado de la ejecución

El playbook se ejecutó correctamente en ambos servidores:

```
server1 : ok=7 changed=0 unreachable=0 failed=0
server2 : ok=7 changed=0 unreachable=0 failed=0
```

No se presentaron errores durante la ejecución.

## Evidencia de ejecución

<img width="1130" height="1027" alt="image" src="https://github.com/user-attachments/assets/bfa46273-c8e6-4a80-9050-d52c1c97eea4" />


