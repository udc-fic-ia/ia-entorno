# Instalación / Configuración entorno IA / 2023-2024 - Windows
-------------------------------------------------------------------------------

## Descargar y copiar el SW 

> NOTA: Se recomienda utilizar un usuario de Windows sin espacios en el nombre 
  para evitar problemas con Maven.

- Descargar y descomprimir en `C:\software` el siguiente software
    - Maven 3.9.x o superior 
        + https://maven.apache.org/download.cgi
        + Descargar el "Binary zip archive"

- Descargar e instalar Eclipse Temurin (proyecto open source de Java SE basado en OpenJDK)
    - https://adoptium.net
    - Descargar el instalador .msi para Windows para la versión 8 (requerida por el software OpenESB)
    - Descargar el instalador .msi para Windows para la versión 17 (LTS) 
    - Instalar usando las opciones por defecto

- Descargar e instalar IntelliJ IDEA
    - https://www.jetbrains.com/es-es/idea/download
        + Se puede utilizar la versión Community (libre) o la versión Ultimate
          (solicitando una licencia para estudiantes según se indica en
          https://www.jetbrains.com/es-es/community/education/#students).
      - Instalar usando las opciones por defecto.
        
## Descargar y descomprimir los ejemplos de la asignatura (rs-java-examples y ws-movies-repo)

> Disponibles en moodle

- Descargar `rs-javaexamples-3.7.0-src.zip` en `C:\software` y descomprimir.

- Descargar `ws-movies-3.7.0-repo.zip` en la carpeta `.m2\repository` del directorio HOME del usuario y descomprimir. 
  
## Establecer variables de entorno

- Ir a "Panel de Control > Sistema > Configuración avanzada del sistema > Variables de entorno ..."

- En la sección "Variables de usuario para `<user>`", crear las siguientes
  variables de entorno (para cada una pulsar en "Nueva ...", introducir el 
  nombre y el valor, y pulsar "Aceptar")
    - Nombre: `JAVA_HOME`
        + Valor: Directorio donde se instaló Eclipse Temurin (JDK 17)
        + Por ejemplo:`C:\Program Files\Eclipse Adoptium\jdk-17.0.8.7-hotspot`
    - Nombre: `MAVEN_HOME`
        + Valor: Directorio donde se descomprimió Maven
        + Por ejemplo: `C:\software\apache-maven-3.9.3`
    - Nombre: `MAVEN_OPTS`
        + Valor: `-Xms512m -Xmx1024m`

- En la sección "Variables de usuario para `<user>`", modificar la variable de
  entorno `PATH`. Para ello hay que seleccionarla, pulsar en "Editar..." y 
  añadir al principio de su valor (sin borrar su valor antiguo):
  
  `%JAVA_HOME%\bin;%MAVEN_HOME%\bin;`
  
> NOTA: Si la variable de entorno PATH no existiese, entonces habría que 
    crearla procediendo de igual forma que se hizo con las variables anteriores.
    
- Cerrar todos los terminales y abrir terminales nuevos

- Comprobar que el entorno ha quedado correctamente configurado comprobando 
  salidas de los siguientes comandos:
  
```shell    
    java -version
    mvn -version
```
    
## Inicialización de datos de ejemplo y compilación de los ejemplos

- Inicialización de la base de datos y compilación de los ejemplos
    - Por defecto crea la base de datos Apache Derby embebida (es lo que usaremos)
    - NOTA: En el caso de querer trabajar contra MySQL, sería necesario
      utilizar el perfil -P mysql, y disponer de un servidor MySQL configurado

```shell
    cd C:/software/rs-javaexamples-3.7.0
    mvn install
    cd C:/software/rs-javaexamples-3.7.0/rs-movies/rs-movies-service
    mvn sql:execute
```

## Instalación y configuración básica de Git
> NOTA: Este paso no es necesario si ya utilizó y configuró Git en otras asignaturas

- Descargar e instalar Git
    - https://git-scm.com/downloads
    - Hacer clic en "Windows" para descargar.
    - Instalar con las opciones por defecto.

- Configuración básica

> NOTA: `$GIT_HOME` debe sustituirse por la ruta donde se instaló git.

    - Ejecutar git-bash (`$GIT_HOME/git-bash.exe`) y desde ese intérprete de comandos ejecutar:

```shell
    git config --global user.email "your_email@udc.es"
    git config --global user.name "Your Name"
```

> El siguiente comando ilustra como configurar Sublime como editor por defecto de Git, aunque se puede utilizar otro editor instalado en el sistema operativo.

```shell
    git config --global core.editor "'C:\Program Files\Sublime Text\sublime_text.exe' -w"
```

## Creación y configuración de claves SSH
> NOTA: Este paso no es necesario si ya utilizó Git en otras asignaturas

- Desde el intérprete de comandos git-bash ejecutar:

> Genera las claves en la ruta por defecto (%USERPROFILE%/.ssh) y con los nombres  por defecto

```shell
    ssh-keygen -t rsa -b 4096 -C "your_email@udc.es"
```    

## Añadir clave SSH a GitHub
> NOTA: Este paso no es necesario si ya utilizó GitHub en otras asignaturas.

- Acceder a [https://github.com/settings/keys](https://github.com/settings/keys).
- Clic en "New SSH Key" para añadir una nueva clave SSH.
- En el campo "Title" ponerle un nombre.
- En el campo "Key" copiar la clave pública, es decir, el contenido del fichero
  `$HOME/.ssh/id_rsa.pub`
- Clic en "Add SSH key".

- Comprobar conexión SSH con el servidor de git y añadirlo a la lista de hosts
  conocidos

> Contestar "yes" a "Are you sure you want to continue connecting (yes/no)?"

```shell
    ssh -T git@github.com
```
    
## Instalación de una herramienta cliente gráfica para Git

- Puede utilizarse cualquier herramienta cliente (https://git-scm.com/downloads/guis)

