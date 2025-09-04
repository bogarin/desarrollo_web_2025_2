---
marp: true
theme: default
class: invert
paginate: true
---

# Patrones en una aplicación: Desarrollo, Comunicación y Despliegue

---
Introducción

Cuando hablamos de "patrones" en una aplicación completa no nos referimos únicamente a los patrones de diseño (código). Una aplicación moderna suele combinar patrones de desarrollo, patrones de comunicación y patrones de despliegue. Cada nivel aborda problemas diferentes: el primero la estructura del código, el segundo la interacción entre componentes o servicios, y el tercero la entrega, operación y disponibilidad del sistema.

---

1. Patrones en el desarrollo (código / implementación)

Estos patrones guían cómo estructuramos y organizamos el código para mejorar reutilización, mantenibilidad y extensibilidad. Muchos provienen del clásico catálogo "Gang of Four" (GoF) y se complementan con prácticas modernas.

Categorías y ejemplos:

Patrones creacionales

Singleton — Garantiza una única instancia global (ej.: gestor de configuración, pool simple). Cuidado: abuso puede dificultar pruebas y paralelismo.

Factory / Abstract Factory — Encapsulan la creación de objetos complejos o familias de productos.

Builder — Construcción paso a paso de objetos complejos (útil para objetos inmutables o con muchos parámetros opcionales).

---

Patrones estructurales

Adapter — Hace compatibles interfaces distintas.

Decorator — Añade funcionalidades a objetos sin modificar su código base.

Facade — Simplifica el acceso a subsistemas complejos mediante una interfaz unificada.

Patrones de comportamiento

---

Observer — Notificaciones entre objetos (ideal para eventos dentro de la misma aplicación).

Strategy — Selección de algoritmos en tiempo de ejecución.

Command — Encapsula operaciones como objetos (útil en colas de tareas, undo/redo).

---

Ejemplo práctico (microservicio de pagos):

Factory para instanciar distintos gateways de pago (Stripe, PayPal, pasarela local).

Observer para notificar a facturación y notificaciones cuando se confirma un pago.

Command para encolar operaciones de reintento o conciliación.

---

Consejos de uso:

Prefiere patrones simples y comprensibles; evita "overengineering".

Escribe pruebas unitarias que validen los puntos de extensión (factories, strategies, etc.).

2. Patrones de comunicación (entre módulos / servicios)

Se aplican cuando la aplicación está distribuida o se compone de varios módulos que deben interoperar. Abordan latencia, tolerancia a fallos, consistencia y escalabilidad.

---

Patrones comunes:

API Gateway — Punto único de entrada para clientes; hace enrutamiento, autenticación y composición de respuestas.

BFF (Backend for Frontend) — Backends adaptados a necesidades específicas de cada cliente (web, móvil).

Service Discovery — Localización dinámica de servicios en entornos elásticos.

Circuit Breaker — Previene fallos en cascada cuando un servicio dependiente está degradado.

Event-Driven Architecture — Comunicación mediante eventos (Kafka, RabbitMQ, MQTT), favorece desacoplamiento.

---

CQRS (Command Query Responsibility Segregation) — Separación de modelos de lectura y escritura para optimizar rendimiento y escalabilidad.

Database per Service — Cada microservicio gestiona su propia persistencia para reducir acoplamiento.

Ejemplo práctico (e‑commerce):

Los clientes llaman al API Gateway.

Al crear un pedido se publica un evento PedidoCreado en Kafka.

Servicios de inventario, pago y notificaciones consumen ese evento y actúan de forma asíncrona.

---

Consideraciones arquitectónicas:

Diseño basado en eventos facilita escalado y resiliencia, pero añade complejidad en la consistencia eventual y observabilidad.

CQRS es útil cuando las cargas de lectura y escritura tienen requisitos muy distintos.

---

3. Patrones de despliegue (infraestructura / operación)

Estos patrones pertenecen al dominio de DevOps y cloud: cómo empaquetas, despliegas, actualizas y operas la aplicación.

Patrones y prácticas clave:

Monolithic Deployment — Despliegue de la aplicación como un único artefacto (útil en etapas tempranas o para equipos pequeños).

Microservice Deployment — Cada servicio se despliega y escala de forma independiente.

Blue-Green Deployment — Dos entornos (blue/green) para cero downtime durante despliegues.

---

Canary Release — Rollout progresivo a un subconjunto de usuarios para validar la nueva versión.

Rolling Update — Actualización gradual de réplicas para minimizar impacto.

Sidecar Pattern — Contenedores auxiliares (telemetría, proxy, seguridad) colocados junto al servicio principal.

Service Mesh — Gestión de la comunicación entre servicios (reintentos, circuit breaking, mTLS) con proxies (por ejemplo, Istio o Linkerd).

---

Ejemplo práctico:

Microservicios en Kubernetes.

Sidecar para exportar métricas a Prometheus y para realizar mTLS.

Canary para validar la versión del servicio de pagos con 5% del tráfico antes del rollout completo.

Buenas prácticas de despliegue:

Automatiza pipelines (CI/CD) y agrega pruebas de integración y contratos.

Ten monitoreo, trazabilidad distribuida (tracing) y alertas configuradas antes de hacer despliegues canary/blue‑green.

---

| Nivel        | Patrones principales                                      | Ejemplo práctico                                |
|--------------|-----------------------------------------------------------|-------------------------------------------------|
| Desarrollo   | Singleton, Factory, Observer, Strategy, Command, Decorator | Creación dinámica de gateways de pago           |
| Comunicación | API Gateway, Event-Driven, CQRS, Service Discovery, BFF   | Kafka para `PedidoCreado` y consumidores        |
| Despliegue   | Blue-Green, Canary, Rolling Update, Sidecar, Service Mesh  | Kubernetes + Sidecars + Canary Releases         |

---

Cuándo usar cada tipo de patrón

Patrones de desarrollo: siempre que busques claridad, reutilización y testeabilidad dentro del código.

Patrones de comunicación: cuando el sistema está distribuido o cuando necesitas tolerancia a fallos y escalabilidad entre componentes.

Patrones de despliegue: cuando quieras asegurar disponibilidad, reducir downtime y automatizar la entrega en entornos productivos.

Recomendaciones prácticas

Empieza simple. Diseña primero con patrones de desarrollo claros; introduce microservicios y patrones de comunicación solo si la complejidad y el equipo lo justifican.

Observabilidad. Antes de adoptar arquitecturas distribuidas, ten logging, métricas y tracing implementados.

---

Automatiza despliegues. Implementa CI/CD y políticas de despliegue (canary, blue‑green) para reducir riesgos.

Documenta decisiones. Mantén una "decision log" (ADR — Architectural Decision Records) para registrar por qué se eligió un patrón.

---

Fuentes y lecturas recomendadas

Gamma, E., Helm, R., Johnson, R., & Vlissides, J. (1995). Design Patterns: Elements of Reusable Object‑Oriented Software (GoF).

Fowler, M. Patterns of Enterprise Application Architecture.

Richardson, C. Microservices Patterns.

Humble, J., & Farley, D. Continuous Delivery.

Documentación oficial de Kubernetes, Istio y herramientas de mensajería como Apache Kafka.