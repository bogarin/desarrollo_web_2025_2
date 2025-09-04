---
marp: true
theme: default
class: invert
paginate: true
---

# ¿Cuál es la diferencia entre patrones de diseño y arquitectura?

---

## Arquitectura de Software

Qué es:
Es la visión de alto nivel del sistema completo: cómo se organizan los módulos, capas, servicios y cómo se comunican entre ellos.

Propósito:
Define la estructura global, los componentes principales y las reglas de interacción.

---

Nivel: Macro (visión de “mapa del sistema”).

Ejemplos de arquitecturas:

Monolítica

N-Capas

Cliente/Servidor

Microservicios

Event-driven

Serverless

Hexagonal / Clean Architecture

---

### Ejemplo

Un e-commerce que decide implementar microservicios, donde cada dominio (carrito, pagos, usuarios, inventario) es un servicio independiente.

---

## Patrones de Diseño

Qué es:
Son soluciones recurrentes a problemas comunes en el diseño de software a nivel de componentes o interacción de objetos.

Propósito:
Reutilizar soluciones probadas para problemas técnicos específicos.

---

Nivel: Micro (en la implementación).

Ejemplos de patrones de diseño clásicos (GoF):

Singleton (un único objeto global).

Factory Method (crear objetos sin exponer lógica de creación).

Observer (notificación a múltiples suscriptores).

Strategy (intercambiar algoritmos en tiempo de ejecución).

---

### Ejemplo

Dentro del microservicio de pagos, se usa un patrón Observer para que cuando un pago se confirme, se notifique automáticamente al servicio de facturación y al de notificaciones.

---

### Diferencia principal

| Aspecto   | Arquitectura                         | Patrones de diseño                        |
|-----------|--------------------------------------|-------------------------------------------|
| Nivel     | Alto nivel (macro)                   | Bajo nivel (micro)                         |
| Alcance   | Todo el sistema o aplicación         | Un módulo, clase o conjunto pequeño de objetos |
| Enfoque   | Organización, comunicación, distribución | Reutilización de soluciones en la implementación |
| Ejemplos  | Microservicios, Monolito, N-Capas, Serverless | Singleton, Factory, Observer, Strategy |

---

__La arquitectura__ es el plano general de una ciudad.

__Los patrones de diseño__ son las técnicas de construcción que usas dentro de los edificios.
