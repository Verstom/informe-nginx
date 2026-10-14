# Práctica: Servidores web con Nginx utilizando Docker

## 1. Título

**Creación y personalización de dos servidores web con Nginx mediante contenedores Docker**

## 2. Tiempo de duración

Tiempo aproximado: 90 minutos.

## 3. Fundamentos

Para realizar esta práctica es necesario conocer qué es un servidor web, para qué sirve Nginx y cómo funciona Docker. Estos conceptos permiten entender cómo se pueden crear y utilizar páginas web sin tener que instalar todos los componentes directamente en el computador.

Un **servidor web** es un programa que recibe solicitudes de un navegador y responde enviando el contenido de una página. Por ejemplo, cuando escribimos una dirección en Chrome y aparece un sitio web, existe un servidor que entrega los archivos necesarios para mostrar esa página.

**Nginx** es un servidor web que permite publicar páginas y entregar contenido a los usuarios. Puede trabajar con archivos HTML, imágenes, hojas de estilo y otros recursos de una página web. En esta práctica se utilizó Nginx para crear dos páginas diferentes: una con información institucional y otra con información personal.

**Docker** es una herramienta que permite ejecutar aplicaciones dentro de contenedores. Un contenedor incluye lo necesario para ejecutar un programa de manera aislada de otros servicios. Esto facilita las pruebas y permite utilizar diferentes aplicaciones en un mismo computador sin tener que instalarlas de la forma tradicional.

Una imagen de Docker contiene los elementos necesarios para crear un contenedor. En este caso se utilizó la imagen oficial de Nginx para crear dos contenedores independientes. Aunque ambos utilizan el mismo servidor web, cada uno tiene su propio nombre, configuración de ejecución y página HTML.

También es importante comprender el uso de los puertos. Un servidor Nginx utiliza normalmente el puerto 80 dentro del contenedor. Sin embargo, para acceder a los dos servidores desde el mismo computador, se asignaron los puertos 8089 y 8090 del equipo. De esta manera, la dirección `http://localhost:8089` permite visualizar el primer servidor y `http://localhost:8090` permite visualizar el segundo.

<p align="center">
  <img src="capturas/fig_esquema.png" alt="Esquema de los dos servidores web" style="max-width:800px;">
</p>

**Figura 3-1. Esquema de los dos servidores web**

Cuando el usuario escribe una dirección en el navegador, la solicitud llega al puerto del equipo, Docker la redirige al puerto 80 del contenedor correspondiente y Nginx responde entregando el archivo `index.html`. Este recorrido se muestra en la siguiente figura.

<p align="center">
  <img src="capturas/fig_flujo.png" alt="Flujo de una solicitud al servidor Nginx" style="max-width:800px;">
</p>

**Figura 3-2. Recorrido de una solicitud desde el navegador hasta la página**

Por último, los archivos HTML permiten definir la estructura y el contenido de las páginas. Para personalizarlas, se copiaron los archivos `index.html` originales de los contenedores al computador, se editaron en Visual Studio Code y luego se copiaron nuevamente a sus respectivos contenedores.

Con esta práctica pude relacionar el uso de la terminal, la edición de archivos HTML y la administración de contenedores. Además, comprobé que dos servidores web pueden ejecutarse al mismo tiempo utilizando diferentes puertos.

## 4. Conocimientos previos

Para realizar esta práctica fue necesario tener conocimientos básicos sobre los siguientes temas:

- Comandos básicos de Linux y Git Bash.
- Manejo de carpetas y archivos desde la terminal.
- Uso de un navegador web.
- Edición de archivos HTML en Visual Studio Code.
- Conceptos básicos de servidores web.
- Uso de Docker Desktop y de la terminal para ejecutar comandos.
- Conocimiento de las direcciones `localhost` y de los puertos de acceso.

## 5. Objetivos a alcanzar

- Implementar dos contenedores con Nginx utilizando Docker.
- Asignar puertos diferentes para acceder a cada servidor web.
- Manipular los archivos `index.html` de los dos contenedores.
- Publicar una página con información institucional y otra con información personal.
- Comprobar mediante el navegador que ambos servidores funcionan correctamente.
- Registrar el procedimiento y los resultados mediante capturas de pantalla.

## 6. Equipo necesario

- Computador con sistema operativo Windows.
- Docker Desktop instalado y en funcionamiento (Docker versión 29.6.1).
- Git Bash para ejecutar los comandos.
- Visual Studio Code para editar los archivos HTML y Markdown.
- Navegador web, como Google Chrome.
- Conexión a Internet para descargar la imagen de Nginx y consultar documentación.
- Imagen de Docker `nginx`.

## 7. Material de apoyo

- Documentación oficial de Docker: https://docs.docker.com/
- Documentación oficial de Nginx: https://nginx.org/en/docs/
- Documentación de Docker sobre la ejecución de contenedores: https://docs.docker.com/engine/containers/run/
- Guía de la asignatura y plantilla proporcionada por el docente: https://github.com/maguaman2/informe-tendencias

## 8. Procedimiento

### Paso 1. Iniciar Docker Desktop

Primero abrí Docker Desktop y esperé a que el servicio estuviera funcionando. Después abrí Git Bash para ejecutar los comandos de la práctica.

Para comprobar que Docker estaba disponible, utilicé:

```bash
docker --version
```

Este comando muestra la versión instalada de Docker.

<p align="center">
  <img src="capturas/im1.png" alt="Verificación de la versión de Docker" style="max-width:800px;">
</p>

**Figura 8-1. Verificación de la versión de Docker**

### Paso 2. Crear el primer contenedor Nginx

Ejecuté el siguiente comando para crear el primer servidor web:

```bash
docker run -d --name nginx1 -p 8089:80 nginx
```

Con este comando se creó un contenedor llamado `nginx1`. El puerto 8089 del computador quedó conectado con el puerto 80 del contenedor, donde funciona Nginx. Como la imagen `nginx` no estaba descargada, Docker la descargó automáticamente.

### Paso 3. Crear el segundo contenedor Nginx

Después ejecuté:

```bash
docker run -d --name nginx2 -p 8090:80 nginx
```

Así se creó un segundo contenedor llamado `nginx2`, utilizando el puerto 8090 del computador. Se asignó un puerto diferente para poder acceder a los dos servidores al mismo tiempo.

<p align="center">
  <img src="capturas/Im2.png" alt="Creación de los contenedores nginx1 y nginx2" style="max-width:800px;">
</p>

**Figura 8-2. Creación de los contenedores nginx1 y nginx2**

### Paso 4. Comprobar los contenedores

Para revisar que los contenedores estuvieran ejecutándose, utilicé:

```bash
docker ps
```

En el resultado comprobé que aparecían los contenedores `nginx1` y `nginx2`, junto con sus puertos asignados (se puede ver en la parte superior de la Figura 8-4).

Además, abrí en el navegador `http://localhost:8090` y comprobé que el servidor respondía con la página de bienvenida que Nginx trae por defecto, antes de modificarla.

<p align="center">
  <img src="capturas/Im3.png" alt="Página de bienvenida por defecto de Nginx" style="max-width:800px;">
</p>

**Figura 8-3. Página de bienvenida por defecto de Nginx**

### Paso 5. Copiar los archivos HTML al computador

Para modificar las páginas, primero copié los archivos originales de Nginx desde cada contenedor:

```bash
docker cp nginx1:/usr/share/nginx/html/index.html ./index1.html
docker cp nginx2:/usr/share/nginx/html/index.html ./index2.html
```

Los archivos `index1.html` e `index2.html` quedaron en mi carpeta de usuario, desde donde pude abrirlos con Visual Studio Code mediante el comando `code index1.html`.

<p align="center">
  <img src="capturas/Im4.png" alt="Contenedores en ejecución y copia de los archivos HTML" style="max-width:800px;">
</p>

**Figura 8-4. Contenedores en ejecución y copia de los archivos HTML**

### Paso 6. Personalizar la página institucional

Abrí el archivo `index1.html` en Visual Studio Code y escribí una primera versión del contenido institucional.

<p align="center">
  <img src="capturas/Im5.png" alt="Primera versión del archivo HTML institucional" style="max-width:800px;">
</p>

**Figura 8-5. Primera versión del archivo HTML institucional**

Luego corregí el archivo y lo dejé con la información institucional del Instituto, el área de Desarrollo de Software y una breve descripción de la práctica.

<p align="center">
  <img src="capturas/Im7.png" alt="Versión final del archivo HTML institucional" style="max-width:800px;">
</p>

**Figura 8-6. Versión final del archivo HTML institucional**

Después guardé los cambios con `Ctrl + S` y copié el archivo actualizado al primer contenedor:

```bash
docker cp index1.html nginx1:/usr/share/nginx/html/index.html
```

<p align="center">
  <img src="capturas/Im6.png" alt="Copia del archivo index1.html al contenedor nginx1" style="max-width:800px;">
</p>

**Figura 8-7. Copia del archivo index1.html al contenedor nginx1**

### Paso 7. Comprobar la primera página web

Abrí el navegador e ingresé a la siguiente dirección:

http://localhost:8089

Comprobé que Nginx mostraba el contenido institucional que había preparado.

<p align="center">
  <img src="capturas/Im10.png" alt="Página institucional en el navegador" style="max-width:800px;">
</p>

**Figura 8-8. Página institucional ejecutada en Nginx**

### Paso 8. Personalizar la página personal

Luego abrí `index2.html` en Visual Studio Code y lo edité para mostrar una página personal con información del estudiante y de los temas que está aprendiendo.

<p align="center">
  <img src="capturas/Im9.png" alt="Código HTML de la página personal" style="max-width:800px;">
</p>

**Figura 8-9. Edición del archivo HTML personal**

Guardé los cambios con `Ctrl + S` y actualicé el archivo del segundo contenedor mediante el siguiente comando:

```bash
docker cp index2.html nginx2:/usr/share/nginx/html/index.html
```

<p align="center">
  <img src="capturas/Im8.png" alt="Copia del archivo index2.html al contenedor nginx2" style="max-width:800px;">
</p>

**Figura 8-10. Copia del archivo index2.html al contenedor nginx2**

### Paso 9. Comprobar la segunda página web

Finalmente, ingresé a:

http://localhost:8090

Verifiqué que apareciera la página personal y que el contenido fuera diferente al del primer servidor.

<p align="center">
  <img src="capturas/Im11.png" alt="Página personal en el navegador" style="max-width:800px;">
</p>

**Figura 8-11. Página personal ejecutada en Nginx**

## 9. Resultados esperados

Al finalizar la práctica, se esperaba tener dos contenedores Nginx ejecutándose al mismo tiempo, cada uno con un puerto diferente y una página HTML personalizada.

Los resultados obtenidos fueron los siguientes:

- Se crearon los contenedores `nginx1` y `nginx2` (Figuras 8-2 y 8-4).
- Se asignó el puerto 8089 al primer servidor y el puerto 8090 al segundo.
- Se editaron los archivos HTML desde Visual Studio Code (Figuras 8-6 y 8-9).
- Se publicó una página institucional en el primer contenedor.
- Se publicó una página personal en el segundo contenedor.
- Se comprobó desde el navegador que las dos páginas se podían abrir por separado.

Las capturas finales de la práctica son las siguientes:

<p align="center">
  <img src="capturas/Im10.png" alt="Resultado final: servidor 1 en localhost:8089" style="max-width:800px;">
</p>

**Figura 9-1. Resultado final: página institucional en `localhost:8089`**

<p align="center">
  <img src="capturas/Im11.png" alt="Resultado final: servidor 2 en localhost:8090" style="max-width:800px;">
</p>

**Figura 9-2. Resultado final: página personal en `localhost:8090`**

En conjunto, las capturas del apartado 8 y estos resultados permiten comprobar que los dos servidores fueron creados y personalizados correctamente.

## 10. Bibliografía

Docker, Inc. (s. f.). *Docker documentation*. https://docs.docker.com/

Docker, Inc. (s. f.). *Run containers*. Docker Docs. https://docs.docker.com/engine/containers/run/

Nginx, Inc. (s. f.). *Nginx documentation*. https://nginx.org/en/docs/