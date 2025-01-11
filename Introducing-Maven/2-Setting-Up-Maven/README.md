### 1. **Requisitos Previos**

Maven es una aplicación basada en Java, por lo que necesita el JDK instalado.

- **Versión Requerida:** Maven 3.6 requiere JDK 1.7 o superior.
- **Variable JAVA_HOME:** Debe apuntar a la ubicación del JDK instalado.**Ejemplo (Windows):Ejemplo (Mac/Linux):**

    ```
    set JAVA_HOME=C:\Program Files\Java\jdk1.8.0_144
    
    ```

    ```bash
    export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_144/Contents/Home
    
    ```


---

### 2. **Descarga de Maven**

- Visitar [Apache Maven Download](http://maven.apache.org/download.html).
- Descargar el archivo binario `.zip` o `.tar.gz` correspondiente al sistema operativo.

**Ejemplo:**

```
apache-maven-3.6.1-bin.zip

```

Descomprimir el archivo en una ubicación como:

- **Windows:** `C:\tools\maven`
- **Mac:** `$HOME/tools/maven`

---

### 3. **Estructura del Directorio de Maven**

El directorio descomprimido incluye:

- **`bin`:** Contiene los ejecutables (`mvn.cmd`, `mvn.sh`) para ejecutar Maven.
- **`conf`:** Archivos de configuración, como `settings.xml`.
- **`lib`:** Bibliotecas esenciales para el funcionamiento de Maven.
- **`boot`:** Incluye el archivo `plexus-classworlds-2.5.2.jar` usado para gestionar el cargador de clases.

---

### 4. **Configuración del Sistema**

### **Windows**

1. Mover el directorio de Maven a `C:\tools\maven`.
2. Agregar la carpeta `bin` de Maven a la variable de entorno `PATH`:
    - Abrir **"Editar las variables del sistema"**.
    - Editar la variable `PATH` y agregar:

        ```
        C:\tools\maven\bin
        
        ```


### **Mac/Linux**

1. Mover el directorio a `$HOME/tools/maven`.
2. Editar el archivo `~/.bash_profile` y agregar:

    ```bash
    export PATH=$HOME/tools/maven/bin:$PATH
    
    ```


---

### 5. **Variable MAVEN_OPTS**

Para evitar errores de memoria en proyectos grandes, se recomienda establecer la variable `MAVEN_OPTS`:

```bash
export MAVEN_OPTS="-Xmx512m"

```

---

### 6. **Verificación de la Instalación**

Abrir una terminal y ejecutar:

```bash
mvn -v

```

**Salida esperada:**

```
Apache Maven 3.6.1
Java version: 1.8.0_144
OS name: "windows 10"

```

---

### 7. **Configuración Adicional con `settings.xml`**

Maven utiliza el archivo `settings.xml` para configuraciones globales y específicas del usuario.

### Ubicación:

- **Global:** `conf/settings.xml` (dentro del directorio de Maven).
- **Usuario:** `~/.m2/settings.xml` (directorio del usuario).

**Ejemplo de archivo `settings.xml`:**

```xml
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
 xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
 http://maven.apache.org/xsd/settings-1.0.0.xsd">
  <localRepository>/path/to/local/repo</localRepository>
  <interactiveMode>true</interactiveMode>
  <offline>false</offline>
</settings>

```

---

### 8. **Configuración de Proxy**

Si se requiere acceso a Internet a través de un proxy:

```xml
<proxies>
  <proxy>
    <id>example-proxy</id>
    <active>true</active>
    <protocol>http</protocol>
    <host>proxy.example.com</host>
    <port>8080</port>
    <username>proxyuser</username>
    <password>somepassword</password>
  </proxy>
</proxies>

```

---

### 9. **Comandos Útiles de Maven**

- **Ver versión:** `mvn -v`
- **Ayuda:** `mvn -h` o `mvn --help`
- **Evaluar configuración:**

    ```bash
    mvn help:evaluate -Dexpression=settings.localRepository
    
    ```


---

### Conclusión

Configurar Maven es un proceso sencillo si se siguen los pasos adecuados. Tener el entorno correctamente configurado garantiza una gestión eficiente de dependencias y proyectos. Los siguientes capítulos profundizarán en la estructura de proyectos Maven y cómo aprovechar sus características avanzadas.