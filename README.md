# Crear un Proyecto Maven con Pruebas Unitarias (JUnit 5)

Este documento proporciona una guía rápida para crear un proyecto Maven desde cero con soporte para pruebas unitarias utilizando JUnit 5.

## 1. Crear el Proyecto Maven

Ejecuta el siguiente comando en la terminal para generar un nuevo proyecto Maven:

```sh
mvn archetype:generate -DgroupId=com.ejemplo -DartifactId=mi-proyecto -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

## 2. Acceder al Directorio del Proyecto

```sh
cd mi-proyecto
```

## 3. Configurar `pom.xml` para JUnit 5

Abre el archivo `pom.xml` y asegúrate de incluir la dependencia de JUnit 5:

```xml
<dependencies>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
        <version>5.9.0</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-engine</artifactId>
        <version>5.9.0</version>
    </dependency>
</dependencies>
```

## 4. Crear una Clase Calculadora

En la carpeta `src/main/java/com/ejemplo`, crea el archivo `Calculadora.java`:

```java
package com.ejemplo;

public class Calculadora {
    public int sumar(int a, int b) {
        return a + b;
    }
    
    public int restar(int a, int b) {
        return a - b;
    }
    
    public int multiplicar(int a, int b) {
        return a * b;
    }
    
    public int dividir(int a, int b) {
        if (b == 0) {
            throw new IllegalArgumentException("No se puede dividir por cero");
        }
        return a / b;
    }
}
```

## 5. Crear una Clase de Prueba para Calculadora

En la carpeta `src/test/java/com/ejemplo`, crea el archivo `CalculadoraTest.java`:

```java
package com.ejemplo;

import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.Test;

class CalculadoraTest {
    private final Calculadora calculadora = new Calculadora();

    @Test
    void testSuma() {
        assertEquals(5, calculadora.sumar(2, 3), "2 + 3 debe ser 5");
    }
    
    @Test
    void testResta() {
        assertEquals(1, calculadora.restar(3, 2), "3 - 2 debe ser 1");
    }
    
    @Test
    void testMultiplicacion() {
        assertEquals(6, calculadora.multiplicar(2, 3), "2 * 3 debe ser 6");
    }
    
    @Test
    void testDivision() {
        assertEquals(2, calculadora.dividir(6, 3), "6 / 3 debe ser 2");
    }
    
    @Test
    void testDivisionPorCero() {
        Exception exception = assertThrows(IllegalArgumentException.class, () -> calculadora.dividir(6, 0));
        assertEquals("No se puede dividir por cero", exception.getMessage());
    }
}
```

## 6. Ejecutar las Pruebas

Para ejecutar las pruebas unitarias, usa el siguiente comando:

```sh
mvn test
```

## 7. Construir el Proyecto

Para compilar y generar el `.jar`, ejecuta:

```sh
mvn clean package
```

El archivo `.jar` generado estará en la carpeta `target/`.

## 8. Ejecutar el Proyecto

Si la aplicación genera un `.jar` ejecutable, puedes correrlo con:

```sh
java -jar target/mi-proyecto-1.0-SNAPSHOT.jar
```

---
¡Tu proyecto Maven con JUnit 5 ya está listo!
