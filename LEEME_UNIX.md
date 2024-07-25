# Instalación / Configuración entorno IA / 2024-2025 - Linux / Mac OS
-------------------------------------------------------------------------------

## Descargar y copiar el SW
  
- [Linux] 
    - Descargar y descomprimir en `$HOME/software` el siguiente software
        - Maven 3.9.x o superior 
            - https://maven.apache.org/download.cgi
            - Descargar el "Binary tar.gz archive".
        - IntelliJ IDEA 
            - https://www.jetbrains.com/es-es/idea/download
            - Se puede utilizar la versión Community (libre) o la versión Ultimate
              (solicitando una licencia para estudiantes según se indica en
              https://www.jetbrains.com/es-es/community/education/#students).
        - Eclipse Temurin (proyecto open source de Java SE basado en OpenJDK)
            - https://adoptium.net
            - Descargar el archivo .tar.gz de la versión 8 (necesaria para el software OpenESB).
            - Descargar el archivo .tar.gz de la versión 21 (última versión LTS).

- [macOS] 
    - Descargar y descomprimir en `$HOME/software`
        - Maven 3.9.x o superior 
            - https://maven.apache.org/download.cgi
            - Descargar el "Binary tar.gz archive"
    - Descargar e instalar
        - IntelliJ IDEA 
            - https://www.jetbrains.com/es-es/idea/download
            - Se puede utilizar la versión Community (libre) o la versión Ultimate
              (solicitando una licencia para estudiantes según se indica en
              https://www.jetbrains.com/es-es/community/education/#students).
            - Instalar usando las opciones por defecto.
        - Eclipse Temurin (proyecto open source de Java SE basado en OpenJDK)
            - https://adoptium.net
            - Descargar el instalador .pkg de la versión 8 e instalar usando las opciones por defecto (necesaria para el software OpenESB).
            - Descargar el instalador .pkg de la versión 21 (LTS) e instalar usando las opciones por defecto.

      
## Descargar y descomprimir los ejemplos de la asignatura (rs-java-examples y ws-movies-repo)

> Disponibles en moodle

- Descargar `rs-javaexamples-3.8.0-src.tar.gz` y `ws-movies-3.8.0-repo.tar.gz` en `$HOME/software`

```shell
    cd $HOME/software
    tar zxf rs-javaexamples-3.8.0-src.tar.gz
    cd $HOME/.m2/repository
    tar zxf $HOME/software/ws-movies-3.8.0-repo.tar.gz
```
  
## [Linux] Establecer variables de entorno
- Añadir al fichero `$HOME/.bashrc` lo siguiente 

> NOTA: Los valores de las variables JAVA_HOME, MAVEN_HOME e IDEA_HOME deben sustituirse por los 
  directorios donde se haya descomprimido Maven e IntelliJ IDEA, e instalado Eclipse Temurin respectivamente

```shell
    # Eclipse Temurin
    export JAVA_HOME=$HOME/software/jdk-21.0.3+9
    PATH=$JAVA_HOME/bin:$PATH

    # Maven
    MAVEN_HOME=$HOME/software/apache-maven-3.9.8
    PATH=$MAVEN_HOME/bin:$PATH
    export MAVEN_OPTS="-Xms512m -Xmx1024m"

    # IntelliJ IDEA
    IDEA_HOME=$HOME/software/idea
    PATH=$IDEA_HOME/bin:$PATH    
```

- Cerrar todos los terminales y abrir terminales nuevos

- Comprobar que el entorno ha quedado correctamente configurado comprobando 
  salidas de los siguientes comandos
  
```shell
    which java
    which mvn
    which idea.sh
```

## [macOS] Establecer variables de entorno
> NOTA: asumiendo que la aplicación Terminal use el shell de inicio de sesión,
éste será "zsh" (macOS 10.15 o superior) o "bash" (versiones anteriores de macOS).

- Añadir al fichero `$HOME/.zshrc` (macOS 10.15 o superior) o
  `$HOME/.bash_profile` (versiones anteriores de macOS) lo siguiente:

> NOTA:  Los valores de las variables MAVEN_HOME y JAVA_HOME deben sustituirse por 
los directorios donde se haya descomprimido Maven e instalado Eclipse Temurin respectivamente

```shell
    # Eclipse Temurin
    export JAVA_HOME=/Library/Java/JavaVirtualMachines/temurin-21.jdk/Contents/Home
    PATH=$JAVA_HOME/bin:$PATH

    # Maven
    MAVEN_HOME=$HOME/software/apache-maven-3.9.8
    PATH=$MAVEN_HOME/bin:$PATH
    export MAVEN_OPTS="-Xms512m -Xmx1024m"
```

- Cerrar todos los terminales y abrir terminales nuevos

- Comprobar que el entorno ha quedado correctamente configurado comprobando 
  salidas de los siguientes comandos
  
```shell
    which java
    which mvn
```

## Inicialización de datos de ejemplo y compilación de los ejemplos

- Inicialización de la base de datos y compilación de los ejemplos
  - Por defecto crea la base de datos Apache Derby embebida (es lo que usaremos)
  - NOTA: En el caso de querer trabajar contra MySQL, sería necesario 
    utilizar el perfil -P mysql, y disponer de un servidor MySQL configurado

```shell
    cd $HOME/software/rs-javaexamples-3.8.0
    mvn install
    cd $HOME/software/rs-javaexamples-3.8.0/rs-movies/rs-movies-service
    mvn sql:execute
```

## Instalación y configuración básica de Git
> NOTA: Este paso no es necesario si ya utilizó Git en otras asignaturas.

- Instalación en Linux
    - https://git-scm.com/downloads
    - Hacer clic en "Linux/Unix" y seguir las instrucciones según la distribución de linux utilizada.

- Instalación en macOS
    - https://git-scm.com/downloads
    - Hacer clic en "MacOs". En la siguiente pantalla hacer clic en "installer"
      dentro de la sección "Binary Installer" y descargar la última versión del instalador .dmg.
    - Instalar con las opciones por defecto.

- Configuración básica (Linux y macOS)

```shell
    git config --global user.email "your_email@udc.es"
    git config --global user.name "Your Name"
```

> El siguiente comando ilustra como configurar Sublime como editor por defecto de Git, aunque se puede utilizar otro editor instalado en el sistema operativo.

```shell
    git config --global core.editor "subl -w"
```

## Creación y configuración de claves SSH
> NOTA: Este paso no es necesario si ya utilizó Git en otras asignaturas.

- Desde un terminal ejecutar:

> Generar las claves en la ruta por defecto ($HOME/.ssh) y con los nombres
por defecto

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

- Comprobar conexión SSH con el servidor de git y añadirlo a la lista de hosts conocidos.

> Contestar "yes" a "Are you sure you want to continue connecting (yes/no)?"

```shell
    ssh -T git@github.com
```

## Instalación de una herramienta cliente gráfica para Git

- Puede utilizarse cualquier herramienta cliente (https://git-scm.com/downloads/guis)
