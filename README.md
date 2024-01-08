# Learning Project: Docker Basics

Este proyecto es un ejemplo práctico para entender los conceptos básicos de Docker. Consiste en una aplicación simple que lista y crea "chanchitos felices" utilizando una API construida en Node.js y una base de datos MongoDB.

## Archivos en el Proyecto

- `Dockerfile` y `Dockerfile.dev`: Estos archivos contienen las instrucciones para construir las imágenes Docker para producción y desarrollo, respectivamente.
- `docker-compose.yml` y `docker-compose-dev.yml`: Estos archivos Docker Compose definen cómo se deben ejecutar los servicios de nuestra aplicación en un entorno de producción y desarrollo.
- `index.js`: El archivo principal de la aplicación Node.js.
- `package.json` y `package-lock.json`: Estos archivos definen las dependencias del proyecto Node.js.

## Conceptos Básicos de Docker

- **Imágenes Docker**: Plantillas inmutables utilizadas para crear contenedores. En este proyecto, se utilizan imágenes para Node.js y MongoDB.
- **Contenedores Docker**: Instancias ejecutables de imágenes que aíslan la aplicación y sus dependencias. Cada servicio en Docker Compose corre en su propio contenedor.
- **Dockerfile**: Un script de instrucciones utilizado para construir una imagen Docker.
- **Docker Compose**: Una herramienta para definir y ejecutar aplicaciones Docker multi-contenedor. Utiliza el archivo `docker-compose.yml` para configurar los servicios de la aplicación.
- **Volúmenes**: Utilizados para la persistencia de datos. En este proyecto, se utiliza un volumen para la base de datos MongoDB.

## Funcionamiento Interno del Proyecto

Una vez que se ejecutan los comandos para levantar el proyecto, sucede una serie de pasos internos que permiten que la aplicación se ejecute correctamente:

1. **Ejecución del Comando de Docker Compose:**
   - Al ejecutar `docker-compose -f docker-compose-dev.yml up`, Docker Compose lee el archivo de configuración especificado (en este caso, `docker-compose-dev.yml`).

2. **Creación de Imágenes:**
   - Docker Compose inicia la construcción de las imágenes necesarias para los servicios definidos en el archivo de configuración.
   - Para el servicio `chanchito`, Docker construye una imagen basada en el `Dockerfile.dev`, que contiene todas las dependencias y el entorno necesario para ejecutar la aplicación Node.js.
   - Para el servicio `monguito`, Docker utiliza la imagen preexistente de MongoDB (`mongo`), que ya está optimizada para su uso.

3. **Creación de Contenedores:**
   - Una vez que las imágenes están listas, Docker Compose crea contenedores a partir de estas imágenes.
   - Cada contenedor es una instancia ejecutable de su imagen correspondiente, configurada según lo definido en el archivo Docker Compose (puertos, volúmenes, variables de entorno, etc.).

4. **Levantamiento de Servidores y Conexiones:**
   - El contenedor del servicio `chanchito` inicia la aplicación Node.js, que se ejecuta en el servidor interno y escucha en el puerto mapeado (3000).
   - El contenedor del servicio `monguito` inicia el servidor de MongoDB, que escucha en el puerto mapeado (27017).
   - Estos contenedores están conectados a través de una red interna, lo que permite a la aplicación Node.js comunicarse con MongoDB para realizar operaciones de base de datos.

5. **Acceso y Uso de la Aplicación:**
   - Una vez que ambos servicios están activos, la aplicación está lista para ser accedida desde un navegador o cliente API en `localhost:3000`.
   - Las operaciones realizadas en la aplicación (como listar o crear "chanchitos felices") son manejadas por la aplicación Node.js, que interactúa con la base de datos MongoDB para almacenar o recuperar información.

Este proceso automatizado facilita la implementación y gestión de aplicaciones compuestas por múltiples servicios, asegurando que todos los componentes necesarios estén configurados y ejecutándose juntos de manera coherente.

## Cómo ejecutar el Proyecto

1. Construir las imágenes: Ejecutar `docker-compose -f docker-compose-dev.yml build` para el entorno de desarrollo.
2. Iniciar los servicios: Ejecutar `docker-compose -f docker-compose-dev.yml up` para levantar la aplicación y la base de datos.
3. Acceder a la aplicación: Navegar a `localhost:3000` para interactuar con la aplicación.


Para más detalles y un tutorial guiado, visitar: [Aprende Docker ahora! curso completo gratis desde cero!](https://www.youtube.com/watch?v=4Dko5W96WHg&ab_channel=HolaMundo).
