# Análisis de Estilo de Código – Checkstyle Report

**Proyecto:** Administración de Parqueadero Java  
**Fecha de análisis:** 4 de diciembre de 2025  
**Herramienta:** Maven Checkstyle Plugin (Checkstyle)

---

## 📊 Resumen Ejecutivo

El análisis de Checkstyle se ejecutó sobre el código fuente del proyecto, verificando principalmente reglas de estilo de código, formateo, nomenclatura y documentación.

| Métrica                | Valor                        |
|------------------------|------------------------------|
| Archivos analizados    | 4 (`Carro`, `Puesto`, `Parqueadero`, `Main`) |
| Advertencias totales   | 746                          |
| Errores (severidad “Error”) | 20 (todas por longitud de línea) |

### Reglas con más violaciones

| Regla / Categoría       | Descripción breve                                 | Cantidad aprox. |
|-------------------------|---------------------------------------------------|------------------|
| `Indentation`           | Niveles de sangría incorrectos                    | ~368             |
| `ParenPad`              | Espacios incorrectos junto a paréntesis          | ~121             |
| `WhitespaceAround`      | Falta de espacios alrededor de operadores/palabras clave | ~84      |
| `WhitespaceAfter`       | Falta de espacio después de comas/palabras clave | ~31              |
| `LeftCurly`             | Posición incorrecta de la llave `{`              | ~51              |
| `LineLength`            | Líneas con más de 100 caracteres (Error)         | 20               |
| Reglas de Javadoc       | Falta o mal formateo de comentarios Javadoc      | ~38              |
| Reglas de nombres       | Nombres de parámetros/variables fuera de convención | ~16           |

> **Conclusión rápida:**  
> El código funciona, pero hay mucha **deuda de estilo**: principalmente problemas de **identación, espacios, llaves y Javadoc**.

---

## 📈 Análisis por Clase

### 1. ✅ Clase `Carro.java`

| Métrica             | Valor  |
|---------------------|--------|
| Advertencias totales| 53     |
| Severidad Error     | Algunas por longitud de línea |

**Problemas principales:**

- Indentación inconsistente en atributos y métodos.
- Uso de espacios extra dentro de paréntesis, por ejemplo: `if ( condicion )` en lugar de `if (condicion)`.
- Nombres de parámetros como `pPlaca`, `pHora`, `pHoraSalida` que no siguen camelCase simple recomendado (`placa`, `hora`, `horaSalida`).
- Llaves `{` en línea distinta a la forma sugerida por el estilo de Google.
- Detalles de Javadoc:
  - Falta de línea en blanco antes de `@param` y `@return`.
  - Resúmenes sin punto final.
- Algunas líneas que superan el límite de 100 caracteres.

**Estado:**  
⚠️ La lógica es sencilla y clara, pero el formato todavía no cumple las reglas del estándar configurado.

---

### 2. ⚠️ Clase `Puesto.java`

| Métrica             | Valor  |
|---------------------|--------|
| Advertencias totales| 71     |
| Severidad Error     | Algunas por longitud de línea |

**Problemas principales:**

- Indentación de atributos y métodos no alineada.
- Llaves de apertura en línea aparte o mal posicionadas.
- Espacios incorrectos en paréntesis y alrededor de operadores.
- Falta de consistencia en Javadoc (estructura de comentarios y resúmenes).
- Nombres que podrían ajustarse mejor a camelCase y convenciones de Google.

**Estado:**  
⚠️ Clase relativamente pequeña, pero con el mismo patrón de problemas de estilo que el resto del proyecto.

---

### 3. 🔴 Clase `Parqueadero.java`

| Métrica             | Valor    |
|---------------------|----------|
| Advertencias totales| 514      |
| Severidad Error     | Varias por longitud de línea |

**Problemas principales:**

- Es el archivo con **más violaciones** de todo el proyecto.
- Indentación incorrecta en:
  - Atributos.
  - Bloques `if/else`, `for`, `while`.
  - Cierres de llaves de métodos y clases.
- Llaves `{` en la siguiente línea, o desalineadas respecto al bloque.
- `for` sin llaves `{}` en algunos casos, lo que activa la regla `NeedBraces`.
- Espacios incorrectos en:
  - Condiciones de `if`.
  - Cabeceras de bucles.
  - Llamadas a métodos.
- Nombres de parámetros como `pPlaca`, `pTarifa`, `pPuesto`, `pPosicion` y variables como `nHoras`, que no se ajustan a las convenciones de nombres.
- Declaración de arreglos como `Puesto puestos[]` en lugar de `Puesto[] puestos`.
- Varias líneas muy largas (más de 100 caracteres), especialmente:
  - Mensajes de consola.
  - Concatenaciones de cadenas.
  - Cálculos complejos en una sola línea.
- Javadoc:
  - Métodos públicos sin documentación.
  - Falta de punto final en el resumen.
  - Falta de línea en blanco antes de `@param`, `@return`.

**Estado:**  
🚨 Es el **principal foco de deuda de estilo** del proyecto. La lógica es extensa y el formato actual dificulta la lectura y el mantenimiento.

---

### 4. ⚠️ Clase `Main.java`

| Métrica             | Valor  |
|---------------------|--------|
| Advertencias totales| 108    |
| Severidad Error     | Varias por longitud de línea |

**Problemas principales:**

- Falta de Javadoc:
  - En la clase.
  - En el método `main`.
- Indentación incorrecta en:
  - El bloque `do { ... } while (...);`
  - El `switch` del menú y cada `case`.
- `switch` sin caso `default`.
- Un `case` con **fallthrough** (sin `break` ni comentario explicando que es intencional).
- Líneas muy largas en mensajes de texto y concatenaciones.
- Problemas de espacios:
  - Falta de espacio alrededor de `+` en concatenaciones.
  - Falta de espacios después de ciertas palabras clave.

**Estado:**  
⚠️ Es la clase de interfaz de usuario por consola. Funciona, pero el estilo es mejorable para hacer el menú más claro y mantenible.

---

## 🧩 Principales Categorías de Problemas (Resumen)

1. **Indentación (`Indentation`)**
   - Problema más frecuente.
   - Afecta todos los archivos.
   - Dificulta seguir la estructura de métodos, condicionales y ciclos.

2. **Paréntesis y espacios (`ParenPad`, `WhitespaceAround`, `WhitespaceAfter`)**
   - Espacios de más o de menos dentro de paréntesis y alrededor de operadores.
   - Hace que el código se vea inconsistente.

3. **Longitud de línea (`LineLength`)**
   - 20 líneas exceden el límite de 100 caracteres.
   - Ocurre sobre todo en:
     - Mensajes largos de `System.out`.
     - Concatenaciones de texto.
     - Expresiones complejas en una sola línea.

4. **Javadoc**
   - Clases y métodos públicos sin documentación.
   - Comentarios con formato incorrecto:
     - Falta de punto final en el resumen.
     - Falta de línea en blanco antes de las etiquetas `@param` y `@return`.

5. **Nomenclatura**
   - Prefijos como `pPlaca`, `pTarifa`, `nHoras`.
   - No se ajustan al camelCase simple que recomiendan las guías de estilo de Java/Google.

6. **Estructuras de control**
   - `switch` sin `default` y con `fallthrough` no documentado.
   - `for` sin llaves `{}` en algunos puntos.

---

## 🛠️ Áreas de Mejora y Acciones Propuestas

### 1. Formateo automático según estándar

**Acción recomendada:**

- Configurar el IDE (IntelliJ, Eclipse, VS Code) para usar el formato **Google Java Style** o el mismo perfil que usa Checkstyle.
- Aplicar **Reformat Code** a todo el proyecto.

**Impacto:**

- Reducir de golpe la mayor parte de:
  - Problemas de indentación.
  - Posición de llaves.
  - Espacios alrededor de operadores y paréntesis.

---

### 2. Ajustar nombres de parámetros y variables

**Acción recomendada:**

- Cambiar nombres como:
  - `pPlaca` → `placa`
  - `pHora` → `hora`
  - `pTarifa` → `tarifa`
  - `nHoras` → `horas` o `numeroHoras`

**Impacto:**

- Cumplir las reglas de nombrado de Checkstyle.
- Hacer el código más legible y estándar para otros desarrolladores.

---

### 3. Dividir líneas largas

**Acción recomendada:**

- Para líneas > 100 caracteres:
  - Dividir mensajes largos en varias partes.
  - Extraer expresiones complejas en variables intermedias.

**Ejemplo:**

```java
System.out.println(
    "Mensaje muy largo que se puede dividir "
        + "en varias partes para respetar el límite de longitud.");

### 5. Revisar estructuras de control

**En `Main`:**

- Agregar un `case default` al `switch` del menú.
- Evitar *fallthrough* no intencional:
  - Usar `break` al final de cada `case`.
  - O documentarlo con un comentario si está hecho a propósito.

**En `Parqueadero`:**

- Asegurarse de que todos los `if`, `for` y `while` que controlan lógica importante tengan llaves `{}`.

---

## ✅ Conclusiones

- El análisis de Checkstyle evidencia que el proyecto tiene una **base funcional**, pero con una **alta cantidad de detalles de estilo pendientes**.
- La mayoría de problemas no afectan la ejecución, pero sí la:
  - legibilidad,  
  - mantenibilidad,  
  - y el cumplimiento de estándares profesionales.

Con acciones relativamente simples:

1. Formateo automático del código.  
2. Corrección de nombres de parámetros y variables.  
3. Ajuste de líneas largas.  
4. Completar y pulir Javadocs.  
5. Ordenar estructuras de control (`switch`, `for`, `if`).  

se puede reducir drásticamente el número de advertencias.

En resumen, el proyecto está **correcto a nivel funcional**, pero el uso de Checkstyle demuestra la necesidad de **pulir el estilo de código** para alinearse con buenas prácticas de desarrollo profesional.
