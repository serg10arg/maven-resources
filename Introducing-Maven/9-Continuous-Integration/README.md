### **Introducción a la Integración Continua**

La **Integración Continua (Continuous Integration o CI)** es una práctica esencial en el desarrollo de software que permite a los desarrolladores integrar cambios en un repositorio común varias veces al día. Cada integración desencadena un proceso automatizado que:

1. Compila el código.
2. Ejecuta pruebas.
3. Genera un nuevo artefacto.

La CI detecta errores en etapas tempranas, facilitando una resolución ágil.

### **Flujo de Trabajo en CI**

1. **Subida del Código**: Los desarrolladores integran cambios en un sistema de control de versiones (p. ej., Git o SVN).
2. **CI Server**: Detecta los cambios, descarga el código y ejecuta el proceso de construcción.
3. **Publicación**: Si la construcción es exitosa, los artefactos generados se publican en un repositorio o servidor de pruebas.
4. **Notificaciones**: El estado del build se comunica al equipo de desarrollo.

### **Herramientas Populares**

- **Jenkins**: Una herramienta de código abierto que se integra bien con Maven.
- Otras herramientas: Bamboo, TeamCity, y GitLab.

### **Instalación de Jenkins**

1. **Descargar Jenkins**:
    - Obtén la versión WAR desde https://jenkins.io/download/.
    - Guarda el archivo en `c:\tools\jenkins`.
2. **Ejecutar Jenkins**:

    ```bash
    java -jar jenkins.war
    
    ```

3. **Configuración Inicial**:
    - Accede a `http://localhost:8080` en tu navegador.
    - Introduce la contraseña del archivo `initialAdminPassword`.
    - Instala los plugins sugeridos.
    - Crea un usuario administrador con nombre y contraseña.

### **Proyecto Maven para Jenkins**

1. **Repositorio de Ejemplo**:
    - Utiliza el repositorio [gswm-jenkins](https://github.com/bava/gswm-jenkins).
    - Haz un fork del proyecto para personalizarlo.
2. **Configuración del Proyecto**:
    - Crea un nuevo proyecto tipo "Freestyle".
    - Configura el URL del proyecto GitHub.

### **Configuración de Jenkins con Maven**

1. **Gestión de Código Fuente**:
    - Selecciona **Git** e introduce el URL del repositorio clonado.
    - Añade credenciales de GitHub (usuario y contraseña).
2. **Configuración del Trigger**:
    - Habilita "Poll SCM" con la expresión `H/15 * * * *` para verificar cambios cada 15 minutos.
3. **Paso de Construcción**:
    - Añade el comando Maven `clean install` para compilar el proyecto.

    ```xml
    <goals>
        clean install
    </goals>
    
    ```

4. **Acciones Post-Construcción**:
    - **Archivar Artefactos**: Archiva los archivos `.jar` generados.
    - **Publicar Resultados de Pruebas JUnit**: Configura la ruta `target/surefire-reports/*.xml`.

### **Ejecución del Job de Construcción**

1. En el tablero de Jenkins, selecciona "Build Now" para iniciar el proceso de construcción.
2. **Historial de Builds**:
    - Accede a la salida de la consola para revisar el progreso.
    - Al finalizar, consulta los artefactos y resultados de pruebas.

### **Fragmento de Configuración en Jenkins**

Ejemplo de configuración de `pom.xml` para integrar Maven:

```xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>gswm-jenkins</artifactId>
    <version>1.0-SNAPSHOT</version>
</project>

```

### **Conclusión**

Este capítulo aborda:

- Los fundamentos de CI.
- La instalación y configuración de Jenkins.
- La integración de Maven con Jenkins para automatizar procesos de construcción y pruebas.

Al implementar CI, los equipos de desarrollo pueden mejorar la eficiencia, reducir riesgos y detectar problemas en etapas tempranas. Esta práctica es esencial para proyectos ágiles y modernos.