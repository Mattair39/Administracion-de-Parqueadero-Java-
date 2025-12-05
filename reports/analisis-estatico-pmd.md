````markdown
# Análisis Estático - PMD Report

**Proyecto:** Administración de Parqueadero Java  
**Fecha de análisis:** 5 de diciembre de 2025  
**Herramienta:** PMD 6.55.0

---

## 📊 Resumen Ejecutivo

| Métrica | Valor |
|--------:|:-----|
| **Violaciones totales** | **10** |
| **Prioridad 3** | 4 |
| **Prioridad 4** | 6 |
| **Archivos afectados** | Carro.java, Main.java, Parqueadero.java |

**Principales hallazgos:** imports innecesarios, variables locales/privadas sin uso, paréntesis innecesarios y condicionales anidados que pueden colapsarse. Son problemas de calidad y mantenibilidad (prioridad media/baja) que no indican fallos funcionales críticos.

---

## 🔍 Violations By Priority

### Priority 3

#### Carro.java

| Rule | Violation | Line |
|------|-----------|------:|
| UnusedPrivateField | Avoid unused private fields such as 'horaSalida'. | 18 |

#### Main.java

| Rule | Violation | Line |
|------|-----------|------:|
| UnusedLocalVariable | Avoid unused local variables such as 'ingresos'. | 12 |

#### Parqueadero.java

| Rule | Violation | Line |
|------|-----------|------:|
| UnusedLocalVariable | Avoid unused local variables such as 'maxHoras'. | 402 |
| CollapsibleIfStatements | These nested if statements could be combined | 479–481 |

### Priority 4

#### Main.java

| Rule | Violation | Line |
|------|-----------|------:|
| UnnecessaryImport | Unused import 'java.awt.event.PaintEvent' | 1 |
| UnnecessaryImport | Unused import 'java.util.ArrayList' | 2 |
| UnnecessaryImport | Unused import 'java.util.List' | 3 |

#### Parqueadero.java

| Rule | Violation | Line |
|------|-----------|------:|
| UnnecessaryImport | Unused import 'java.util.List' | 2 |
| UselessParentheses | Useless parentheses. | 277 |
| UselessParentheses | Useless parentheses. | 355 |

---

## 📁 Files

#### Carro.java

| Rule | Violation | Priority | Line |
|------|-----------|---------:|------:|
| UnusedPrivateField | Avoid unused private fields such as 'horaSalida'. | 3 | 18 |

#### Main.java

| Rule | Violation | Priority | Line |
|------|-----------|---------:|------:|
| UnnecessaryImport | Unused import 'java.awt.event.PaintEvent' | 4 | 1 |
| UnnecessaryImport | Unused import 'java.util.ArrayList' | 4 | 2 |
| UnnecessaryImport | Unused import 'java.util.List' | 4 | 3 |
| UnusedLocalVariable | Avoid unused local variables such as 'ingresos'. | 3 | 12 |

#### Parqueadero.java

| Rule | Violation | Priority | Line |
|------|-----------|---------:|------:|
| UnnecessaryImport | Unused import 'java.util.List' | 4 | 2 |
| UselessParentheses | Useless parentheses. | 4 | 277 |
| UselessParentheses | Useless parentheses. | 4 | 355 |
| UnusedLocalVariable | Avoid unused local variables such as 'maxHoras'. | 3 | 402 |
| CollapsibleIfStatements | These nested if statements could be combined | 3 | 479–481 |

---

## ✅ Problemas detectados y correcciones recomendadas

- **Carro.java**
	- Problema: `UnusedPrivateField` — campo `horaSalida` (línea 18).
	- Corrección: eliminar el campo si no se utiliza. Si es necesario en el futuro, documentarlo explícitamente.

- **Main.java**
	- Problemas: `UnnecessaryImport` (`PaintEvent`, `ArrayList`, `List`) y `UnusedLocalVariable` (`ingresos`).
	- Corrección: eliminar los imports y la variable local no usada. Verificar compilación y tests.

- **Parqueadero.java**
	- Problemas: imports no usados (`java.util.List`), `UselessParentheses` (líneas 277 y 355), `UnusedLocalVariable` (`maxHoras`), `CollapsibleIfStatements` (479–481).
	- Corrección:
		- Quitar import no usado.
		- Eliminar o usar `maxHoras` según corresponda.
		- Reemplazar if anidados por condiciones compuestas o guard clauses. Ejemplo:

```java
// Antes
if (condA) {
		if (condB) {
				realizarAccion();
		}
}

// Después
if (condA && condB) {
		realizarAccion();
}
```

		- Quitar paréntesis inútiles donde la precedencia ya es suficiente.

**Validación:** Compilar y ejecutar los tests (`mvn -q test`) después de cada cambio y ejecutar PMD de nuevo para confirmar la reducción de advertencias.

---

## 🛠 Pasos sugeridos

1. Crear branch: `git checkout -b fix/pmd-cleanup`  
2. Aplicar cambios por archivo (eliminar imports/variables, simplificar ifs, quitar paréntesis).  
3. Ejecutar:  
```bash
mvn -q test
```  
4. Ejecutar PMD nuevamente y comprobar que las violaciones hayan disminuido.

---

*Análisis generado por **GitHub Copilot***

*Fecha: 5 de diciembre de 2025*

````

