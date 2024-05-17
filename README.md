# Colecciones

## Configuración

Hay que añadir las siguientes dependencias

### JUnit

#### Dependencia

```xml
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.13.2</version>
    <scope>test</scope>
</dependency>
```

#### Plugin

**ATENCION** - Solo debe haber una etiqueta build en un pom.xml, si quieren configurar varias cosas dentro se deben mantener
en la misma etiqueta build.

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>3.2.5</version>
        </plugin>
    </plugins>
</build>
```

### Slf4j

#### Dependencia

```xml
 <dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-log4j12</artifactId>
    <version>2.0.13</version>
</dependency>
```
#### log4j.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE log4j:configuration SYSTEM "log4j.dtd">

<log4j:configuration debug="true">
    <appender name="fileAppender" class="org.apache.log4j.RollingFileAppender">
        <param name="File" value="out.log"/>
        <layout class="org.apache.log4j.PatternLayout">
            <param name="ConversionPattern" value="%d{yyyy-MM-dd HH:mm:ss} %-5p %c:%L - %m%n" />
        </layout>
    </appender>

    <appender name="consoleAppender" class="org.apache.log4j.ConsoleAppender">
        <param name="Target" value="System.out"/>
        <layout class="org.apache.log4j.PatternLayout">
            <param name="ConversionPattern" value="%d{yyyy-MM-dd HH:mm:ss} %-5p %c:%L - %m%n" />
        </layout>
    </appender>
    <root>
        <priority value="DEBUG" />
        <appender-ref ref="consoleAppender" />
        <appender-ref ref="fileAppender" />
    </root>
</log4j:configuration>
```

### Lobmok

Hay que cargar:

#### Propiedades

```xml
<lombok.version>1.18.30</lombok.version>
<maven-plugin.version>3.8.1</maven-plugin.version>
```

#### Dependencia

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>${lombok.version}</version>
    <scope>provided</scope>
</dependency>
```
#### Plugin

**ATENCION** - Solo debe haber una etiqueta build en un pom.xml, si quieren configurar varias cosas dentro se deben mantener
en la misma etiqueta build.

```xml
<build>
    <pluginManagement>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>${maven-plugin.version}</version>
                <configuration>
                    <annotationProcessorPaths>
                        <path>
                            <groupId>org.projectlombok</groupId>
                            <artifactId>lombok</artifactId>
                            <version>${lombok.version}</version>
                        </path>
                    </annotationProcessorPaths>
                </configuration>
            </plugin>
        </plugins>
    </pluginManagement>
</build>
```

## PRIMERA PARTE (HACER ANTES)

### Ejercicio 1 (1 punto)

Configura JUnit, Lombok y Slf4j, siguiendo las instrucciones anteriores.

Añade anotaciones a las clases del paquete `org.ies.tierno.prog3ev.model` para que generen automáticamente:
- Constructor con todos los campos
- Getters, setters, hashCode, equals...

Crea un logger en la clase Ej1, muestra en pantalla el mensaje "Hola mundo"

### Ejercicio 2 (1 punto)

Añade los siguientes campos a los POJOs del modelo:
- Añade un campo a Videoclub que almacene las películas indexadas por id de película.
- Añade un campo a Pelicula que almacene un listado de actores que actúan en la película.
- Añade un campo a Pelicula que almacence un conjunto no ordenado géneros de esa película.

### Ejercicio 3 (HACER ANTES EJERCICIO 2)  (1 punto)

En el método principal de Ej3:
- Crea una colección de actores (usando la clase Actor), **la colección debe ordenar** los actores por: país, apellidos y nombre
- Añade tres actores a la colección que acabas de crear 
- Recorre la colección mostrando los actores en pantalla

## SEGUNDA PARTE (HACER ANTES LA PRIMERA PARTE)

### Ejercicio 4 (1 punto)

Añade un método a la clase Videoclub que, dado un nif de actor, devuelva las películas en las que aparece dicho actor.

### Ejercicio 5  (1 punto)

Añade un método a la clase Videoclub que, dado un id de película y un nif de actor, devuelva los datos de dicho actor.
En caso de que no exista la película lanza la excepción FilmNotFoundException, en caso de que no actue el actor en la 
película lanza la excepción ActorNotFoundException.

### Ejercicio 6 (1 punto)

Crea los tests unitarios necesarios para cubrir los casos relevantes del método del ejercicio 5

### Ejercicio 7 - STREAMS (1 punto)

Añade un método a la clase Videoclub que, dado un género, devuelve una lista de ids de película de ese género (List<Integer>)

### Ejercicio 8 (1 punto)

Crea los tests unitarios necesarios para cubrir los casos relevantes del método del ejercicio 7

### Ejercicio 9 (2 punto)

Implementa el método `run` del componente VideoclubApp:
- Crea un videoclub hardcodeado (puedes usar el mismo que has creado para el ejercicio 6)
- Bucle de menú con las siguientes opciones:
  - Ver películas de actor
  - Ver actor en película
  - Salir

En caso de excepción muestra al usuario un mensaje informativo. 

