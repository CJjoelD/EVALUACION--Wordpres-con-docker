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
<img width="1901" height="195" alt="image" src="https://github.com/user-attachments/assets/06b042de-ca03-4e9c-b732-382fa2aa7e34" />

phpMyAdmin
<img width="642" height="632" alt="image" src="https://github.com/user-attachments/assets/a660a4a2-79cf-4639-8285-63d5eb7ec882" />

wordpress
<img width="1918" height="1071" alt="image" src="https://github.com/user-attachments/assets/227f680e-b435-4c5a-b834-b68d7b281ac5" />


En esta práctica se implementó un entorno WordPress utilizando contenedores Docker. Se crearon contenedores independientes para MySQL, phpMyAdmin y WordPress, conectados mediante una red Docker personalizada. Además, se utilizaron volúmenes para mantener la persistencia de datos.


11. Conclusión

Con Docker fue posible desplegar rápidamente un entorno funcional de WordPress separando cada servicio en diferentes contenedores. El uso de redes permitió la comunicación entre servicios y los volúmenes garantizaron la persistencia de datos incluso si los contenedores son eliminados.
