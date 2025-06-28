# Proyecto MySQL en Docker

Este proyecto levanta una instancia de MySQL dentro de un contenedor Docker, accesible desde múltiples proyectos gracias a una red compartida (`pereza-network`).

## 🐳 Requisitos

- Docker
- Docker Compose

## 📦 Estructura del proyecto

project_db/
├── docker-compose.yml
└── schemas/ # Directorio que se monta como volumen (persistencia)


## 🚀 Instrucciones
### 1. Crear carpeta para persistencia:
```bash
mkdir schemas
```

### 2. Crear red Docker externa (una sola vez)

```bash
docker network create pereza-network
```

Esto crea una red bridge llamada pereza-network, usada para conectar otros proyectos a esta base de datos.

### 3. Levantar el servicio de base de datos

Desde el directorio de este proyecto:

```bash
docker compose up -d
```

### 4. Configuración de conexión

Desde otros contenedores dentro de la red pereza-network:

    Host: MYSQL
    Puerto: 3306 (puerto interno del contenedor)
    Usuario: root
    Contraseña: admin

Desde tu máquina (localhost):

    Host: localhost
    Puerto: 3307
    Usuario: root
    Contraseña: admin

    ⚠️ Recuerda que los puertos internos (3306) son los usados por otros contenedores; los externos (3307) son para conexión desde tu sistema operativo.

### 5. Conexión desde DBeaver

    Tipo de conexión: MySQL
    Host: localhost
    Puerto: 3307
    Usuario: root
    Contraseña: admin
    Opciones avanzadas:
        allowPublicKeyRetrieval = true
        useSSL = false

