## 1. **Introducción a Maven Release**

El objetivo principal del proceso de liberación en Maven es automatizar las tareas repetitivas y críticas relacionadas con la publicación de software, como:

- Verificar la limpieza del código fuente.
- Actualizar versiones en los archivos `pom.xml`.
- Crear etiquetas en sistemas de control de versiones.
- Generar y desplegar artefactos en repositorios remotos.

---

## 2. **Integración con Nexus**

### 2.1. ¿Qué es Nexus?

Nexus es un gestor de repositorios ampliamente utilizado para:

- Actuar como proxy de repositorios públicos.
- Facilitar la colaboración y el intercambio de artefactos entre equipos.
- Asegurar estabilidad en los procesos de construcción (builds).
- Centralizar la administración de dependencias.

### Ventajas:

- Permite agrupar múltiples repositorios bajo una sola URL.
- Simplifica el cambio de configuraciones para los desarrolladores.
- Proporciona capacidades de búsqueda y alojamiento de sitios generados con Maven.

### 2.2. Instalación de Nexus

1. Descargue la distribución de Nexus desde [Sonatype Nexus](https://help.sonatype.com/repomanager3/download).
2. Extraiga los archivos y colóquelos en `C:\tools\nexus`.
3. Configure JAVA_HOME para usar JDK/JRE versión 8.
4. Ejecute los comandos en la terminal:

    ```bash
    nexus /install Nexus_Repo_Manager
    nexus start
    
    ```

5. Acceda a la interfaz web en `http://localhost:8081/`.

### 2.3. Configuración del Proyecto Maven

Modifique el archivo `pom.xml` para agregar el elemento `distributionManagement`:

```xml
<distributionManagement>
    <repository>
        <id>nexusReleases</id>
        <name>Releases</name>
        <url>http://localhost:8081/repository/maven-releases</url>
    </repository>
    <snapshotRepository>
        <id>nexusSnapshots</id>
        <name>Snapshots</name>
        <url>http://localhost:8081/repository/maven-snapshots</url>
    </snapshotRepository>
</distributionManagement>

```

Configure las credenciales en `settings.xml` para habilitar la autenticación:

```xml
<servers>
    <server>
        <id>nexusReleases</id>
        <username>admin</username>
        <password>admin123</password>
    </server>
    <server>
        <id>nexusSnapshots</id>
        <username>admin</username>
        <password>admin123</password>
    </server>
</servers>

```

---

## 3. **Proceso de Liberación de Proyectos**

### 3.1. Pasos del Proceso

1. Verifique que no haya cambios pendientes en el código fuente.
2. Elimine la etiqueta `SNAPSHOT` del archivo `pom.xml`.
3. Asegúrese de que no existan dependencias SNAPSHOT.
4. Realice un commit de los cambios en el control de versiones.
5. Cree una etiqueta del código fuente.
6. Genere y despliegue el artefacto en el repositorio.
7. Actualice la versión en `pom.xml` para la próxima iteración.

### 3.2. Uso del Plugin de Liberación de Maven

El plugin de liberación de Maven automatiza este proceso. Ejecute el comando:

```bash
mvn release:prepare release:perform

```

### Configuración del Plugin:

Agregue la configuración del plugin en el archivo `pom.xml`:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-release-plugin</artifactId>
            <version>3.0.0</version>
        </plugin>
    </plugins>
</build>

```

---

## 4. **Integración con GitHub**

### 4.1. Instalación de Git

1. Descargue el cliente Git desde [Git SCM](https://git-scm.com/downloads).
2. Verifique la instalación:

    ```bash
    git --version
    
    ```


### 4.2. Configuración de un Repositorio Remoto

1. Cree una cuenta en [GitHub](https://github.com/join).
2. Inicie sesión y cree un nuevo repositorio en [GitHub](https://github.com/new).

### 4.3. Subida del Código Fuente

Ejecute los siguientes comandos para inicializar un repositorio local y vincularlo al remoto:

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/<usuario>/<repositorio>.git
git push -u origin main

```

---

## 5. **Despliegue de Artefactos**

Una vez configurado Nexus y GitHub, despliegue los artefactos ejecutando:

```bash
mvn deploy

```

Verifique los artefactos en la URL de Nexus:

`http://localhost:8081/#browse/browse:maven-releases`.

---

## 6. **Ejemplo Práctico: Ciclo Completo**

1. Configure Nexus y GitHub.
2. Configure el proyecto `pom.xml` y `settings.xml`.
3. Ejecute el comando:

    ```bash
    mvn release:prepare release:perform
    
    ```

4. Verifique los cambios en GitHub y Nexus.

---

## Conclusión

El proceso de liberación con Maven simplifica la gestión de versiones y el despliegue de artefactos, integrando sistemas como Nexus y GitHub para optimizar el flujo de trabajo en proyectos empresariales.