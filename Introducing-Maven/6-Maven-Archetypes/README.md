## **1. Introducción a Maven Archetypes**

- **Definición:** Un arquetipo en Maven es una plantilla preconfigurada para generar proyectos con una estructura estándar.
- **Beneficios:**
    - Acelera la creación de proyectos repetitivos.
    - Establece consistencia en la estructura y configuración de proyectos.
    - Promueve el uso de mejores prácticas dentro de equipos y organizaciones.

Ejemplo:

```bash
mvn archetype:generate

```

El comando anterior inicia un proceso interactivo para seleccionar y usar un arquetipo.

---

## **2. Arquetipos Incorporados**

- Maven incluye cientos de arquetipos listos para usar, adecuados para diversos propósitos.
- Los arquetipos pueden ser descargados desde repositorios locales o remotos.
- El complemento `archetype` proporciona el objetivo `generate`, que permite explorar y seleccionar arquetipos.

### **Ejemplo: Generar Proyecto Web**

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-webapp

```

Proceso interactivo típico:

```
Define value for property 'groupId': : com.example
Define value for property 'artifactId': : my-web-app
Define value for property 'version': 1.0-SNAPSHOT: : <<Enter>>
Define value for property 'package': com.example.webapp: : <<Enter>>

```

### **Estructura generada:**

```
my-web-app/
├── src/
│   ├── main/
│   │   ├── java/
│   │   ├── resources/
│   │   └── webapp/
│       └── WEB-INF/
└── pom.xml

```

---

## **3. Personalización del Proyecto Web**

### **Añadir soporte para servidores web incrustados**

- Modificar el archivo `pom.xml` para incluir el plugin de Jetty:

```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.eclipse.jetty</groupId>
      <artifactId>jetty-maven-plugin</artifactId>
      <version>9.4.12.RC2</version>
    </plugin>
  </plugins>
</build>

```

### **Ejecutar el servidor Jetty**

```bash
mvn jetty:run

```

Resultado: La aplicación está disponible en http://localhost:8080/.

---

## **4. Proyectos Multimódulo**

### **Definición:**

- Los proyectos multimódulo dividen aplicaciones grandes en módulos más pequeños y manejables, como:
    - **Web (WAR):** Interfaz de usuario.
    - **Service (JAR):** Lógica empresarial.
    - **Repository (JAR):** Acceso a datos.

### **Estructura de Proyecto Multimódulo:**

```
parent-project/
├── pom.xml (padre)
├── web-module/
│   └── pom.xml
├── service-module/
│   └── pom.xml
└── repository-module/
    └── pom.xml

```

### **Creación del Proyecto Padre**

```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=parent-project -Dversion=1.0.0-SNAPSHOT -DarchetypeArtifactId=pom-root

```

Archivo `pom.xml` del proyecto padre:

```xml
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>parent-project</artifactId>
  <version>1.0.0-SNAPSHOT</version>
  <packaging>pom</packaging>
  <modules>
    <module>web-module</module>
    <module>service-module</module>
    <module>repository-module</module>
  </modules>
</project>

```

### **Generación de Módulos**

1. **Módulo Web:**

```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=web-module -DarchetypeArtifactId=maven-archetype-webapp

```

1. **Módulo de Servicio:**

```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=service-module -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

```

1. **Módulo de Repositorio:**

```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=repository-module -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

```

---

## **5. Buenas Prácticas**

- **Estandarización Organizacional:** Crear arquetipos personalizados con configuraciones específicas (e.g., CSS corporativo, bibliotecas JavaScript aprobadas).
- **Evitar repetición:** Utilizar el parámetro `DinteractiveMode=false` para agilizar la generación de proyectos.

---

## **6. Conclusión**

Maven Archetypes simplifica la creación y gestión de proyectos, mejorando la eficiencia del desarrollo y garantizando la uniformidad en equipos. Su uso es esencial para iniciar aplicaciones Spring y otros proyectos empresariales de manera eficiente.