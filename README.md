# Proyecto: Taller de Despliegue de Aplicación Web con Spring y Docker

## Descripción General
Este taller consiste en la creación de una aplicación web pequeña utilizando el micro-framework de **Spring**. Posteriormente, construiremos un contenedor Docker para la aplicación, lo configuraremos y desplegaremos localmente. La imagen de Docker será subida a un repositorio en **DockerHub** y, finalmente, desplegaremos el contenedor en una máquina virtual de **AWS**.

## Arquitectura
La arquitectura de este proyecto es una aplicación web sencilla que se ejecuta en un entorno **Docker** y es accesible a través de instancias en una máquina virtual de **AWS**. Los componentes principales incluyen:

- **Aplicación web**: Construida con Spring Framework.
- **Docker**: Para contenerizar y desplegar la aplicación.
- **AWS EC2**: Máquina virtual donde se desplegará la imagen Docker.

## Proceso de Configuración y Compilación
### Prerrequisitos
- **Java 8+** (JDK)
- **Maven** para la gestión de dependencias y compilación
- **Docker** instalado en la máquina local
- Cuenta en **DockerHub**
- **AWS CLI** (opcional para el manejo de instancias EC2)

### Pasos para la Configuración y Compilación Local
1. **Clonar el repositorio**:
    ```bash
    git clone https://github.com/usuario/taller-spring-docker.git
    cd taller-spring-docker
    ```

2. **Compilar el proyecto**:
    ```bash
    mvn clean install
    ```

3. **Ejecutar la aplicación**:
    ```bash
    java -cp "target/classes:target/dependency/*" co.edu.escuelaing.sparkdockerdemolive.RestServiceApplication
    ```

4. **Verificar el acceso a la aplicación**:
   Accede a la URL: [http://localhost:4567/hello](http://localhost:4567/hello)

## Creación y Gestión de la Imagen Docker
### Pasos para Construir la Imagen Docker
1. **Construir la imagen Docker**:
    ```bash
    docker build --tag dockersparkprimer .
    ```

2. **Verificar la imagen creada**:
    ```bash
    docker images
    ```

### Desplegar Contenedores Docker
1. **Crear instancias del contenedor Docker**:
    ```bash
    docker run -d -p 34000:33025 --name firstdockercontainer dockersparkprimer
    docker run -d -p 34001:33025 --name firstdockercontainer2 dockersparkprimer
    docker run -d -p 34002:33025 --name firstdockercontainer3 dockersparkprimer
    ```

2. **Verificar que los contenedores estén corriendo**:
    ```bash
    docker ps
    ```

## Publicación de la Imagen en DockerHub
1. **Iniciar sesión en DockerHub**:
    ```bash
    docker login
    ```

2. **Etiquetar la imagen para DockerHub**:
    ```bash
    docker tag dockersparkprimer usuario/dockerhub-repo:latest
    ```

3. **Subir la imagen al repositorio**:
    ```bash
    docker push usuario/dockerhub-repo:latest
    ```

## Despliegue en AWS
1. **Crear una máquina virtual EC2 en AWS**.
2. **Instalar Docker en la máquina virtual**:
    ```bash
    sudo apt update
    sudo apt install docker.io
    ```

3. **Descargar y ejecutar la imagen desde DockerHub**:
    ```bash
    sudo docker pull usuario/dockerhub-repo:latest
    sudo docker run -d -p 80:33025 usuario/dockerhub-repo:latest
    ```

4. **Verificar que el contenedor esté en ejecución**:
    ```bash
    sudo docker ps
    ```


