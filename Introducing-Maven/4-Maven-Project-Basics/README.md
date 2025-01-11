## **1. Introducción a Maven**

Maven es una herramienta de gestión y construcción de proyectos que proporciona:

- **Estandarización:** Uso de convenciones y una estructura de directorios estándar.
- **Facilidad de integración:** Interfaces uniformes que permiten a los desarrolladores colaborar y moverse entre proyectos con rapidez.

El núcleo de un proyecto Maven es el archivo **`pom.xml`**, donde se define la configuración, dependencias y fases de construcción.

---

## **2. Organización básica de un proyecto Maven**

### **Estructura del proyecto**

Un proyecto Maven típico sigue una estructura estándar como se muestra en la siguiente jerarquía:

```
gswm/
 ├── src/
 │    ├── main/
 │    │    ├── java/             (Código fuente Java principal)
 │    │    ├── resources/        (Recursos como archivos de configuración de Spring)
 │    │    ├── config/           (Archivos de configuración específicos del entorno)
 │    │    └── webapp/           (Archivos web como JSP, CSS, imágenes)
 │    └── test/
 │         ├── java/             (Pruebas unitarias en Java)
 │         └── resources/        (Recursos necesarios para las pruebas)
 ├── target/                     (Artefactos generados como archivos .class o JAR)
 ├── pom.xml                     (Archivo de configuración principal)
 ├── README.txt                  (Información del proyecto)
 └── LICENSE.txt                 (Información de licencia)

```

### **Explicación de directorios clave**

1. **`src/main/java`:** Contiene el código fuente principal.
2. **`src/test/java`:** Incluye las pruebas unitarias escritas en Java.
3. **`src/main/resources`:** Contiene recursos como archivos de configuración (`application.properties`) y plantillas.
4. **`target`:** Carpeta generada que contiene artefactos como archivos `.jar` o `.war`.
5. **`pom.xml`:** Archivo principal donde se gestionan dependencias, configuraciones y propiedades del proyecto.

---

## **3. Configuración del archivo pom.xml**

El archivo `pom.xml` define las características clave del proyecto. Un ejemplo básico es:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <!-- Coordenadas principales del proyecto -->
    <groupId>com.example</groupId>
    <artifactId>my-app</artifactId>
    <version>1.0.0-SNAPSHOT</version>
    <packaging>jar</packaging>

    <!-- Información adicional -->
    <name>My Maven Application</name>
    <url>http://example.com</url>

    <!-- Dependencias -->
    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
            <version>5.3.5</version>
        </dependency>
    </dependencies>
</project>

```

### **Componentes principales**

- **`groupId`:** Identificador único del proyecto (ej. nombre de dominio invertido).
- **`artifactId`:** Nombre del artefacto (por ejemplo, el archivo JAR).
- **`version`:** Versión del proyecto. Usar `SNAPSHOT` indica que está en desarrollo.
- **`dependencies`:** Lista de bibliotecas externas requeridas por el proyecto.

---

## **4. Creación de un proyecto Maven desde cero**

Pasos para configurar un proyecto básico manualmente:

1. Crear un directorio base:

    ```bash
    mkdir gswm
    cd gswm
    ```

2. Crear un archivo `pom.xml` vacío.
3. Configurar la estructura de directorios:

    ```bash
    mkdir -p src/main/java src/test/java
    ```


Resultado:

```
gswm/
 ├── pom.xml
 └── src/
      ├── main/java
      └── test/java

```

---

## **5. Ejemplo práctico: Clase "HelloWorld"**

Crear una clase simple para el proyecto:
**Archivo:** `src/main/java/HelloWorld.java`

```java
public class HelloWorld {
    public void sayHello() {
        System.out.println("Hello World");
    }
}

```

### **Compilación y construcción**

Ejecutar el siguiente comando para compilar y empaquetar el proyecto:

```bash
mvn package

```

Salida esperada:

```
[INFO] Compiling 1 source file to target/classes
[INFO] Building jar: target/gswm-1.0.0-SNAPSHOT.jar
[INFO] BUILD SUCCESS

```

---

## **6. Pruebas unitarias con JUnit**

### **Agregar dependencia JUnit**

Actualizar el archivo `pom.xml` para incluir JUnit como dependencia:

```xml
<dependencies>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.13.2</version>
        <scope>test</scope>
    </dependency>
</dependencies>

```

### **Crear una prueba para la clase "HelloWorld"**

**Archivo:** `src/test/java/HelloWorldTest.java`

```java
import org.junit.Test;
import static org.junit.Assert.*;

public class HelloWorldTest {
    @Test
    public void testSayHello() {
        HelloWorld helloWorld = new HelloWorld();
        helloWorld.sayHello();
        assertTrue(true); // Validación básica
    }
}

```

### **Ejecutar las pruebas**

```bash
mvn test

```

Salida esperada:

```
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0
[INFO] BUILD SUCCESS

```

---

## **7. Buenas prácticas de versionado**

- Formato recomendado: `major.minor.incremental-qualifier` (ej. `1.0.0-SNAPSHOT`).
- Usar `SNAPSHOT` para indicar versiones en desarrollo.

---

## **8. Conclusión**

Este capítulo cubre los fundamentos de un proyecto Maven, desde la estructura de directorios hasta la configuración básica del archivo `pom.xml`. Maven simplifica la gestión de dependencias, la construcción y las pruebas de aplicaciones Java, haciendo que sea una herramienta esencial para proyectos modernos.