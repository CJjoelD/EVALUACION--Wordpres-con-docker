# Implementación de WordPress con Docker

## Introducción

En esta práctica se implementó un entorno WordPress utilizando contenedores Docker. Se crearon contenedores independientes para MySQL, phpMyAdmin y WordPress, conectados mediante una red Docker personalizada. Además, se utilizaron volúmenes para mantener la persistencia de datos.

---

# Objetivos

- Implementar WordPress utilizando Docker.
- Crear una red personalizada para la comunicación entre contenedores.
- Utilizar volúmenes persistentes para almacenar datos.
- Administrar la base de datos mediante phpMyAdmin.

---

# Red Docker Creada

```bash
docker network create wordpress_net
```

---

# Volúmenes Creados

```bash
docker volume create wordpress_data
docker volume create mysql_data
```

---

# Contenedor MySQL

```bash
docker run -d ^
--name mysql_db ^
--network wordpress_net ^
-e MYSQL_ROOT_PASSWORD=1234 ^
-e MYSQL_DATABASE=wordpress ^
-e MYSQL_USER=wpuser ^
-e MYSQL_PASSWORD=wp123 ^
-v mysql_data:/var/lib/mysql ^
-p 3306:3306 ^
mysql:5.7
```

---

# Contenedor phpMyAdmin

```bash
docker run -d ^
--name phpmyadmin ^
--network wordpress_net ^
-e PMA_HOST=mysql_db ^
-e PMA_PORT=3306 ^
-p 8081:80 ^
phpmyadmin/phpmyadmin
```

---

# Contenedor WordPress

```bash
docker run -d ^
--name wordpress ^
--network wordpress_net ^
-e WORDPRESS_DB_HOST=mysql_db:3306 ^
-e WORDPRESS_DB_USER=wpuser ^
-e WORDPRESS_DB_PASSWORD=wp123 ^
-e WORDPRESS_DB_NAME=wordpress ^
-v wordpress_data:/var/www/html ^
-p 8080:80 ^
wordpress
```

---

# Contenedores Utilizados

| Contenedor | Función | Puerto |
|---|---|---|
| mysql_db | Base de datos MySQL | 3306 |
| phpmyadmin | Administración web MySQL | 8081 |
| wordpress | Sitio WordPress | 8080 |

---

# Volúmenes Utilizados

| Volumen | Uso |
|---|---|
| mysql_data | Persistencia de MySQL |
| wordpress_data | Archivos de WordPress |

---

# Diagrama de Contenedores

```text
                 ┌────────────────────┐
                 │    phpMyAdmin      │
                 │   Puerto 8081      │
                 └─────────┬──────────┘
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
┌────────▼────────┐              ┌──────────▼─────────┐
│ wordpress_data  │              │    mysql_data      │
│     Volumen     │              │      Volumen       │
└─────────────────┘              └────────────────────┘
```

---

# Resultados

Se logró implementar correctamente un entorno WordPress funcional utilizando Docker. Los contenedores pudieron comunicarse mediante una red personalizada y los datos fueron almacenados correctamente utilizando volúmenes persistentes.

---

# Conclusión

Con Docker fue posible desplegar rápidamente un entorno funcional de WordPress separando cada servicio en diferentes contenedores. El uso de redes permitió la comunicación entre servicios y los volúmenes garantizaron la persistencia de datos incluso si los contenedores son eliminados.
