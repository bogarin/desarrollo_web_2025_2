---
marp: true
theme: default
class: invert
paginate: true
---

Arquitectura Cliente–Servidor — Desarrollo teórico
1. Introducción y concepto fundamental

El modelo cliente-servidor es un patrón arquitectónico donde las responsabilidades de una aplicación se dividen entre clientes (consumidores de servicios) y servidores (proveedores de servicios).

Cliente: entidad que inicia peticiones para obtener recursos o ejecutar acciones (p. ej. navegador web, app móvil, servicio automatizado).

Servidor: entidad que recibe peticiones, ejecuta lógica y devuelve respuestas (p. ej. servidor HTTP, API, servidor de base de datos).

El propósito del patrón es separar la presentación y la interacción (cliente) de la lógica y el almacenamiento (servidor), lo que facilita mantenimiento, escalabilidad y especialización.

---

2. Historia y evolución breve

Inicios: modelos centralizados (mainframes) y terminales tontos.

Cliente-Servidor clásico: PC con aplicaciones que se conectan a un servidor de archivos o base de datos.

Evolución a 3-capas y n-capas para separar presentación, lógica y persistencia.

Aparición de servicios distribuidos, microservicios y arquitecturas basadas en APIs, impulsadas por la web y la nube.

---

3. Modelo y variantes por capas
3.1 Modelo de 2 capas (cliente ↔ servidor)

Estructura: Cliente <-> Servidor (a menudo el servidor incluye lógica y acceso a datos).

Características: Simplicidad, rápido de implementar; el servidor asume la mayor parte del trabajo.

Limitaciones: Difícil de escalar en grandes sistemas; acoplamiento entre lógica y datos.

---

3.2 Modelo de 3 capas

Capas: Presentación (cliente), Lógica de negocio (servidor de aplicaciones/API), Persistencia (BD).

Beneficios: Separación de responsabilidades, más fácil de escalar y mantener.

Uso típico: Aplicaciones empresariales y web modernas con backend desacoplado.

---

3.3 Modelo n-capas / distribuido

Descripción: Más de tres capas, con servicios especializados: API Gateway, autenticación, caché, colas, microservicios, capas de integración.

Ventajas: Alta escalabilidad, despliegue independiente, resiliencia.

Complejidad: Gestión operativa, observabilidad y testing más complejos.

---

4. Ciclo de petición-respuesta (request–response)

Inicio: El cliente crea y envía una petición (request) al servidor.

Transporte: La petición viaja por la red (TCP/IP, HTTP/HTTPS).

Procesamiento: El servidor recibe, autentica/autoriza, aplica lógica y accede a recursos (BD, cache, servicios).

Respuesta: El servidor envía una respuesta (status, headers, body) al cliente.

Renderizado/consumo: El cliente procesa y muestra o usa la respuesta.

Aspectos relevantes: latencia de red, tiempos de procesamiento en servidor, concurrencia, y manejo de errores (códigos HTTP, retries).

---

5. Protocolos y pila tecnológica

Capa de transporte/Red: TCP/IP (la base), UDP cuando se requiere baja latencia.

Capa de aplicación: HTTP/HTTPS (más común en web), WebSocket (comunicación bidireccional), gRPC (RPC eficiente), GraphQL (consulta flexible).

Formato de datos: JSON, XML, protobuf, YAML.
Elección depende de requisitos de rendimiento, compatibilidad y facilidad de integración.

---

6. Estado: stateless vs stateful

Stateless (sin estado): Cada petición contiene toda la información necesaria; el servidor no guarda contexto entre peticiones. Ej.: REST idealmente stateless.

Ventaja: fácil de escalar horizontalmente.

Stateful (con estado): El servidor mantiene información de sesión entre peticiones (p. ej. sockets persistentes, sesiones en memoria).

Desafío: mantener afinidad y consistencia al escalar; puede requerir session stores (Redis).

Mecanismos comunes para manejar el estado: cookies, tokens JWT (stateless), session stores (Redis, memcached).

---

7. Autenticación, autorización y control de sesiones

Autenticación: comprobar identidad (user/pass, OAuth, SAML, JWT).

Autorización: decidir permisos (roles, scopes).

Sesiones: gestión del estado de autenticación. Técnicas: cookies de sesión (stateful), tokens en cabecera Authorization (bearer/JWT).
Buenas prácticas: transmisión sólo por HTTPS, uso de refresh tokens con cuidado, almacenamiento seguro de secretos.

---

8. Seguridad básica en el modelo cliente-servidor

Transporte seguro: TLS/HTTPS para confidencialidad e integridad.

Entradas validadas: prevenir inyecciones (SQLi, NoSQLi), XSS.

CORS: política de origen cruzado para controlar accesos desde otros dominios.

Control de sesiones: duración, revocación y protección contra fijación de sesión.

Rate limiting y protección contra DDoS: filtrar abusos de petición.

Principio de mínimo privilegio: servicios y procesos con permisos reducidos.

---

9. Rendimiento, escalabilidad y disponibilidad

Escalado vertical: aumentar capacidad de máquina (CPU, RAM).

Escalado horizontal: replicar instancias de servidor y equilibrar carga (load balancers).

Caching: reducir latencia y carga del servidor (CDN, reverse proxy, caches en memoria como Redis).

Balanceo de carga: round-robin, least connections, IP-hash; puede ser a nivel de red (L4) o aplicación (L7).

Alta disponibilidad: replicas, failover, particionamiento de datos, y diseño para tolerancia a fallos.

---

10. Componentes comunes en despliegues modernos

Proxy inverso / reverse proxy: Nginx, HAProxy (terminan TLS, balancean, cachean).

API Gateway: único punto de entrada para APIs (enrutamiento, autenticación, rate limiting).

Service Mesh: para microservicios, maneja observabilidad, seguridad entre servicios.

Colas y eventos: RabbitMQ, Kafka para desacoplar y procesar asíncronamente.

Orquestación de contenedores: Kubernetes para gestionar despliegue y escalado.

---

11. Patrones arquitectónicos relacionados

Proxy / Reverse proxy (p.ej. Nginx delante del app server).

API Gateway (agrega cross-cutting concerns: auth, throttling).

Circuit Breaker (evita cascada de fallos entre servicios).

Backend for Frontend (BFF) (adaptador de API por tipo de cliente).

CQRS y Event Sourcing (separación lectura/escritura y modelado por eventos — en sistemas complejos).

---
12. Microservicios vs Monolito (relación con cliente-servidor)

Monolito: todo el backend en una sola aplicación; simple de desarrollar inicialmente.

Microservicios: múltiples servicios pequeños que se comunican sobre red; mejor para escalado y equipos distribuidos.

Relación con cliente: desde la perspectiva del cliente cambia poco; lo relevante es cómo el servidor (o conjunto de servidores) organiza y expone su API.

---

13. Observabilidad y operación

Para operar sistemas cliente-servidor a producción se necesita:

Logging estructurado (correlación de trazas).

Tracing distribuido (ej. OpenTelemetry) para request flows entre servicios.

Métricas y alertas (Prometheus, Grafana).

Monitoreo de salud (readiness/liveness probes).

---

14. Consideraciones de diseño y buenas prácticas

Diseñar APIs claras y versionadas (por ejemplo, v1 en la ruta).

Mantener contratos estables entre cliente y servidor (documentar con OpenAPI/Swagger / GraphQL schema).

Implementar validaciones en servidor, nunca confiar únicamente en validación del cliente.

Tratar errores y códigos HTTP apropiadamente (4xx cliente, 5xx servidor).

Desacoplar dependencias (uso de colas para trabajo asíncrono).

Aplicar pruebas (unitarias, integración y pruebas de contrato).

---

15. Limitaciones y riesgos

Latencia de red e intermitencia: tratar con retries y backoff exponencial.

Complejidad operativa en arquitecturas distribuidas (observabilidad, despliegue, seguridad).

Consistencia de datos cuando hay réplicas o particionado.

Coste de infraestructura al escalar.

---

16. Glosario rápido

API Gateway: puerta de entrada a múltiples servicios; aplica políticas.

Reverse Proxy: intermediario que recibe peticiones y las reenvía a servidores internos.

Stateless: sin memoria de peticiones previas.

Session store: almacenamiento central para sesiones (ej. Redis).

Load balancer: distribuye tráfico entre instancias.

---

17. Lecturas y recursos recomendados (para profundizar)

Documentación de HTTP/HTTPS y modelos de seguridad.

Guías sobre diseño de APIs (RESTful, GraphQL).

Material sobre patrones de arquitectura distribuida (microservicios, service mesh).

OWASP Top 10 (para seguridad en aplicaciones web).