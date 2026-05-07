# Implementación de WordPress con Docker

## Objetivo
Implementar un entorno WordPress utilizando contenedores Docker.

Objetivo
Implementar WordPress con Docker.
Crear una red personalizada.
Utilizar volúmenes persistentes.
Administrar la base de datos mediante phpMyAdmin.
Contenedores utilizados
Contenedor	Función	Puerto
mysql_db	Base de datos MySQL	         3306
phpmyadmin	Administración web MySQL	 8081
wordpress	Sitio WordPress	             8080
Volúmenes utilizados
Volumen	Uso
mysql_data	Persistencia de MySQL
wordpress_data	Archivos de WordPress

## Red creada

```bash
docker network create wordpress_net

Volúmenes creados

docker volume create wordpress_data
docker volume create mysql_data

Contenedor MySQL
docker run -d --name mysql_db ...
Contenedor phpMyAdmin
docker run -d --name phpmyadmin ...

Contenedor WordPress
docker run -d --name wordpress ...

Diagrama de contenedores
                 ┌────────────────────┐
                 │    phpMyAdmin      │
                 │   Puerto 8081      │
                 └─────────┬──────────┘
                           │
                           │
                    wordpress_net
                           │
         ┌─────────────────┴─────────────────┐
         │                                   │
┌────────▼────────┐              ┌──────────▼─────────┐
│    WordPress    │              │       MySQL        │
│   Puerto 8080   │              │    Puerto 3306     │
└────────┬────────┘              └──────────┬─────────┘
         │                                   │
         │                                   │
┌────────▼────────┐              ┌──────────▼─────────┐
│ wordpress_data  │              │    mysql_data      │
│     Volumen     │              │      Volumen       │
└─────────────────┘              └────────────────────┘



Evidencias
<img width="1918" height="1071" alt="Captura de pantalla 2026-05-07 182353" src="https://github.com/user-attachments/assets/f892f09c-f33a-4a7f-ae63-d44f08a08f57" />
<img width="642" height="632" alt="Captura de pantalla 2026-05-07 182345" src="https://github.com/user-attachments/assets/287f9a1f-a487-457d-84b8-ff4e8dc1543a" />
<img width="1901" height="195" alt="Captura de pantalla 2026-05-07 182319" src="https://github.com/user-attachments/assets/01c503b4-7240-4465-8a06-0504652bba1c" />



En esta práctica se implementó un entorno WordPress utilizando contenedores Docker. Se crearon contenedores independientes para MySQL, phpMyAdmin y WordPress, conectados mediante una red Docker personalizada. Además, se utilizaron volúmenes para mantener la persistencia de datos.


11. Conclusión

Con Docker fue posible desplegar rápidamente un entorno funcional de WordPress separando cada servicio en diferentes contenedores. El uso de redes permitió la comunicación entre servicios y los volúmenes garantizaron la persistencia de datos incluso si los contenedores son eliminados.
