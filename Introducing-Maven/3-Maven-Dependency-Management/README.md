### **1. Introducción a la Gestión de Dependencias**

En proyectos empresariales, es común depender de múltiples bibliotecas de código abierto. Antes de herramientas como Maven, la gestión de dependencias implicaba desafíos como:

- Identificar manualmente dependencias y sus subdependencias.
- Actualizar manualmente las versiones de bibliotecas.
- Incrementar el tamaño de los proyectos al incluir archivos JAR.
- Dificultades para compartir dependencias entre equipos.

**Solución de Maven**: Maven utiliza un enfoque declarativo donde las dependencias se definen en un archivo `pom.xml`. Maven:

- Descarga automáticamente dependencias desde repositorios remotos como **Maven Central**.
- Resuelve subdependencias (transitivas) automáticamente.
- Almacena artefactos descargados en un repositorio local para mejorar la velocidad de compilación.

---

### **2. Configuración de Dependencias en Maven**

### **Archivo POM (`pom.xml`)**

El archivo `pom.xml` es el núcleo de Maven. Aquí se declaran las dependencias usando el formato:

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>5.3.10</version>
    </dependency>
</dependencies>

```

- **groupId**: Identifica la organización que desarrolla el proyecto (e.g., `org.hibernate`).
- **artifactId**: Nombre del artefacto generado (e.g., `hibernate-core`).
- **version**: Versión específica del artefacto (e.g., `5.4.2.Final`).

### **Dependencias Transitivas**

Maven resuelve automáticamente dependencias indirectas (transitivas). Por ejemplo, al usar Hibernate, Maven incluirá automáticamente dependencias como `jboss-logging` y `javassist`.

Ejemplo de exclusión de una dependencia transitoria:

```xml
<dependencies>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.13</version>
        <exclusions>
            <exclusion>
                <groupId>org.hamcrest</groupId>
                <artifactId>hamcrest-core</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
</dependencies>

```

---

### **3. Repositorios Maven**

### **Repositorios Remotos**

El repositorio predeterminado de Maven es **Maven Central**. Sin embargo, pueden configurarse repositorios adicionales, como los de Spring o JBoss:

```xml
<repositories>
    <repository>
        <id>spring_repo</id>
        <url>https://repo.spring.io/release</url>
    </repository>
</repositories>

```

### **Repositorio Local**

Maven almacena dependencias descargadas en un repositorio local (generalmente en `~/.m2/repository`).

### **Repositorios Empresariales**

En entornos empresariales, se usa un repositorio interno (e.g., Nexus, Artifactory) para:

- Cachear artefactos y mejorar la velocidad de descarga.
- Regular los artefactos utilizados en la organización.
- Compartir bibliotecas internas de forma segura.

Configuración en `settings.xml` para un repositorio interno:

```xml
<settings>
    <profiles>
        <profile>
            <id>internal_repo</id>
            <repositories>
                <repository>
                    <id>company_repo</id>
                    <url>http://repo.company.com/maven2</url>
                </repository>
            </repositories>
        </profile>
    </profiles>
    <activeProfiles>
        <activeProfile>internal_repo</activeProfile>
    </activeProfiles>
</settings>

```

---

### **4. Resolución de Conflictos de Dependencias**

### **Mediación de Dependencias**

Cuando varias versiones de una dependencia están presentes, Maven elige:

1. La versión más cercana al proyecto en el árbol de dependencias.
2. Si hay varias versiones a la misma profundidad, se selecciona la primera encontrada.

### **Visualización del Árbol de Dependencias**

El plugin `maven-dependency-plugin` ayuda a visualizar las dependencias:

```bash
mvn dependency:tree

```

Ejemplo de salida:

```
[INFO] com.example:myapp:jar:1.0.0-SNAPSHOT
[INFO] \- junit:junit:jar:4.11:test
[INFO]    \- org.hamcrest:hamcrest-core:jar:1.3:test

```

---

### **5. Buenas Prácticas**

1. **Versiones SNAPSHOT**: Usar versiones con `SNAPSHOT` para indicar que el artefacto está en desarrollo.
2. **Evitar Dependencias No Necesarias**: Excluir dependencias que puedan causar conflictos.
3. **Centralización de Repositorios**: Configurar un repositorio interno para mejorar la seguridad y control.

---

### **6. Ejemplo Práctico: Proyecto Spring**

### **Estructura del POM**

```xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>spring-app</artifactId>
    <version>1.0.0</version>
    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
            <version>5.3.10</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.3.10</version>
        </dependency>
    </dependencies>
</project>

```

### **Ejecutar el Proyecto**

1. Compilar:

    ```bash
    mvn compile
    
    ```

2. Ejecutar Pruebas:

    ```bash
    mvn test
    
    ```


---

### **7. Conclusión**

Maven simplifica la gestión de dependencias en proyectos Java al automatizar la resolución, descarga y mediación de conflictos. Su capacidad para manejar dependencias transitivas y trabajar con repositorios locales y remotos lo hace indispensable en proyectos empresariales.