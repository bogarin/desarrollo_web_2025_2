---
marp: true
theme: default
class: invert
paginate: true
---
<!-- https://web.archive.org/ -->
# 🌐 Desarrollo de Aplicaciones Web
### Unidad 1 – Fundamentos y Arquitecturas Modernas

**Objetivo general de la unidad:** Proveer una base conceptual y práctica sobre la evolución de la Web, elementos de la plataforma web moderna, arquitecturas de software, y conceptos esenciales de seguridad aplicables a aplicaciones web.

---

# 🕹 Evolución de la Web — Web 1.0 (1991–2003)
- **Características:** páginas estáticas, contenido "solo lectura", navegación hipertextual.  
- **Tecnologías:** HTML básico, HTTP 1.0, servidores estáticos (Apache, NCSA).  
- **Ejemplos históricos:** primer sitio del CERN, Geocities.  

**Código representativo (HTML estático):**
```html
<!doctype html>
<html>
  <head><title>Página estática</title></head>
  <body>
    <h1>Bienvenido</h1>
    <p>Contenido estático</p>
  </body>
</html>
```

---

# 🤝 Web 2.0 — La Web Social e Interactiva (2003–2012)
- **Características:** contenido dinámico y generado por usuarios; aplicaciones RIA (Rich Internet Applications).  
- **Tecnología clave:** AJAX (Asynchronous JavaScript and XML) — (patrón para actualizar partes de la página sin recargarla).  
- **Ejemplos:** Facebook, YouTube, Google Maps.

**Ejemplo AJAX / Fetch API (JS):**
```js
fetch('/api/posts')
  .then(res => res.json())
  .then(posts => console.log(posts));
```

---

# 🧠 Web 3.0 — Semántica y Descentralización (2012–2020)
- **Características:** datos enlazados, búsqueda semántica, mayor interoperabilidad entre datos.  
- **Tecnologías:** RDF (Resource Description Framework), SPARQL (consulta semántica), JSON-LD.  
- **Descentralización:** blockchain y contratos inteligentes (p.ej. Ethereum).  
- **Ejemplo aplicado:** Knowledge Graphs, motores de recomendación.


---

**Ejemplo JSON-LD (metadatos semánticos):**
```json
{
  "@context": "https://schema.org",
  "@type": "Person",
  "name": "Ana",
  "jobTitle": "Ingeniera"
}
```

---

# 🤖 Web 4.0 — Web Inteligente e Inmersiva (2020–presente)
- **Características:** IA integrada (modelos generativos, asistentes), interacción multimodal (voz, visión), AR/VR (WebXR), IoT + 5G.  
- **Impacto:** personalización en tiempo real, interfaces conversacionales y experiencias inmersivas.  

**Ejemplo conceptual (pseudo integración IA):**
```js
const respuesta = await openai.chat("Resume la diferencia entre Web3 y Web4");
console.log(respuesta);
```

---

# 🏗 Arquitecturas clásicas: Cliente–Servidor, 2 capas y 3 capas
- **Cliente–Servidor** (modelo básico): Cliente (presentación) solicita recursos al servidor (lógica/datos).  
- **2 capas:** presentación + servidor (datos y lógica en el mismo nivel).  
- **3 capas:** presentación (UI), lógica de negocio (API), persistencia (BD).  
- **Ventaja 3 capas:** separación de responsabilidades, escalabilidad y mantenibilidad.

**Diagrama lógico (texto):**  
`Cliente (UI)  -->  Servidor (API - Lógica)  -->  DB (Persistencia)`

---

# 🧩 Arquitecturas modernas: Microservicios, Serverless, Edge
- **Microservicios** (arquitectura basada en servicios pequeños y autónomos) — (beneficio: despliegue y escalado independiente).  
- **Serverless** (FaaS — Functions as a Service) — (cobro por ejecución, buena para picos y eventos).  
- **Edge Computing** (procesamiento cerca del usuario) — (reduce latencia).  

**Consideraciones:** observabilidad (logs, tracing), orquestación (Kubernetes), API Gateway, tolerancia a fallos.

---

# 📦 Ejemplo práctico — Endpoint REST (Node.js + Express)
```js
// app.js
const express = require('express');
const app = express();

app.get('/api/hello', (req, res) => {
  res.json({ message: 'Hola Mundo desde Node.js' });
});

app.listen(3000, () => console.log('listening on :3000'));
```

**Actividad práctica:** levantar el servidor y consultar `http://localhost:3000/api/hello`.

---

# 📦 Ejemplo práctico — Endpoint REST (Java + Spring Boot)
```java
// HelloController.java
@RestController
public class HelloController {
  @GetMapping("/api/hello")
  public ResponseEntity<Map<String,String>> hello() {
    return ResponseEntity.ok(Collections.singletonMap("message", "Hola Mundo desde Spring Boot"));
  }
}
```

**Actividad práctica:** crear proyecto Spring Boot (start.spring.io), ejecutar y validar endpoint.

---

# 🔒 Seguridad esencial en aplicaciones Web
- **OWASP Top 10** — (lista de riesgos críticos: inyección, XSS, CSRF, etc.).  
- **HTTPS** — (cifrado en transporte con TLS).  
- **Autenticación y autorización:** JWT (JSON Web Token), OAuth2, OpenID Connect.  
- **Buenas prácticas:** validación del lado servidor, escape de salida (output encoding), manejo seguro de sesiones y contraseñas (hashing + salt).

**Ejemplo minimal JWT (payload):**
```json
{
  "sub": "user123",
  "role": "instructor",
  "exp": 1716240000
}
```

---

# 🧪 Actividades prácticas y evaluación (Unidad 1)
**Prácticas (2 horas):**
1. Lab A — Crear y ejecutar endpoint Node.js (Express). (Entrega: repo/Git commit).  
2. Lab B — Crear y ejecutar endpoint Spring Boot. (Entrega: repo/Git commit).  
3. Mini-quiz online (5 preguntas) sobre evolución de la Web y arquitecturas.

**Criterios de evaluación:**
- Funcionamiento del endpoint (40%).  
- Claridad del código y documentación (30%).  
- Respuestas del quiz y participación en clase (30%).

---

# 📚 Recursos y lecturas recomendadas
- W3C — World Wide Web Consortium — https://www.w3.org/  
- MDN Web Docs — https://developer.mozilla.org/  
- OWASP Top Ten — https://owasp.org/www-project-top-ten/  
- Spring Boot Reference — https://spring.io/projects/spring-boot  
- Node.js Documentation — https://nodejs.org/en/docs/  
- Martin Fowler — Patterns of Enterprise Application Architecture (recomendado)

