# Docker M8
##
Introducción a Docker
https://dev.to/pwd9000/introduction-to-github-codespaces-building-your-first-dev-container-69l

## Enlace para generar un clon del repo
https://github.com/ASIXGuine/m8/generate

##Texto de bienvenida
Welcome to Codespaces! You are on our default image. 
   - It includes runtimes and tools for Python, Node.js, Docker, and more. See the full list here: https://aka.ms/ghcs-default-image
   - Want to use a custom image instead? Learn more here: https://aka.ms/configure-codespace

🔍 To explore VS Code to its fullest, search using the Command Palette (Cmd/Ctrl + Shift + P or F1).

📝 Edit away, run your app as usual, and we'll automatically make it available for you to access.

## Enlace para generar un clon del repo
https://github.com/ASIXGuine/m8/generate

## Paso a paso con docker

## Ejecutar el primer docker
   docker run -d --name apache-container -p 8181:80 httpd:latest

## Ejecutar el primer Dockerfile

   ### Configurar el docker file (escribir esto en el archivo Docker file)
   \# Utiliza la imagen oficial de nginx (servidor web) en su versión alpine (más ligera)
   FROM nginx:alpine
   \# Crea un archivo index.html con el contenido "Hola Mundo"
   RUN echo "<h1>Hola Mundo</h1>" > /usr/share/nginx/html/index.html
   \# Inicia el servidor nginx
   CMD ["nginx", "-g", "daemon off;"]

   ### Crear la imagen con su etiqueta (Ejecutar esto n línea de comandos)

   \# Crea la imagen y la etiqueta (atención al punto, que indica donde se encuentra el Dockerfile)
   docker build -t helloworld:latest .

   \# Instacia un contenedor a partir de la etiqueta y le pone el nombre helloWorld-container
   docker run -d --name helloworld-container -p 8383:80 helloworld:latest

   ### Hacer algunas pruebas:
   1. Intentar levantar otra vez un contenedor con las mismas características
      Se puede levantar, pero con otro nombre y en otro puerto
   2. Si queremos que el mismo container sirva por el 8383?
      comandos: docker ps -a, docker kill, docker start docker container prune

   ### Hacer algunas modificaciones en el docker file
   Imaginar que por cualquier motivo, necesitamos que el servidor web sirva por un puerto diferente al 80
   [...] //Tema dekl SED 

## Reorganizar el repositorio
   - Llegdo a este punto, podemos reorganizar el repositorio para separar lo que acabamos de hacer de lo siguiente
   - Crear una carpeta helloworld, y moverlo tood ahí
   - Crear una carpeta videostreamer
   - Matar todos los dockers, colocarse en la carpeta helloworld, y comprobar que seguimos podiendo crear la imagen y desplegar el Docker
   - comandos: docker images, docker container, docker container ls, o list, con --all

## Configurar un contenedor persistente
   Los cambios que hagan en el conenedor sólo se mantienen en el mismo contenedor, y se mantienen después de hacer un kill, o un stop y al reiniciar el contenedor con el comando start, pero es frecuente que a lo largo del ciclo de vida de  un conenedor sea necesario reconstruirlo a partir de actualizaciones de la imagen original.  Para esto es necesario asociar los directiorios que se deseen conservar con una imagen o volumen en el host.  De esta manera, diferentes contenedores generados a partir de la misma imagen, pueden persistir su información

   ### Diferencia entre volumes y bind mount
   Volumes los gestiona Docker.  No hay acceso a los archivos del volumen porque estamos en un docker-indocker, y no tenemos usuario con permisos para acceder a los archivos de los volúmenes
   
   Los bind mount son monstajes de directorios más parecidos a los que se hacen en el sistema operativo.
   ### Opción 1: enlazar un volumen al vuelo ()

      - probar a lanzar un contenedor sin volumen, crear un archivo en la carpeta /usr/share/nginx/html del contenedor,y comprobar que funciona accediendo a ese archivo a través del servidor web. Matar el contendor y prunarlo.  Crear un nuevo conenedor y montarlo don el mismo volumen.  Hacer la misma comprobación (ojo con la caché del navegador).  Cuál es el. resultado?
      - Hacer lo mismo con un contenedor con un volumen montado.  Ver más abajo
      - Comandos: docker volume ls, docker volume inspect [nombre o id del volumen], docker exec -it [nombre/id] sh (o verlo en el plugin de docker)
      - Ejecutar con volumen: docker run -d --name helloworld-container -p 8383:80 -v hwc:/usr/share/nginx/html helloworld:latest
   ### Opción 2: montar un directorio al vuelo

   ## Docker compose
      Como se puede ver, la instanciación de contenedores mediante la línea de comandos se empieza a complicar según los comandos que utilicemos, y a medida que queremos añadirle más caracteríaticas a la imagen.

   ### Juntarlo todo en un único docker compose.
      
      Ahora montaremos un contenedor con las mismas características que el contenedor con el que hemos estado probando, pero lo haremos configurando un archivo docker-compose.yml

   ### Añadir un segundo container al mismo archivo de docker compose
   ### Extra: utilizar el plugin de Visual Studio code para manejar los contenedores

## Configurar un docker con un servidor de streaming de video
   ### Crear el dockerfile






