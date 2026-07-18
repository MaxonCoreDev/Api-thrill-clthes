# Thrill E-commerce API 🛒

[![Java](https://img.shields.io/badge/Java-17-ED8B00?style=flat&logo=openjdk&logoColor=white)](https://openjdk.java.net/)
[![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.4.4-6DB33F?style=flat&logo=spring&logoColor=white)](https://spring.io/projects/spring-boot)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?style=flat&logo=mysql&logoColor=white)](https://www.mysql.com/)
[![Mercado Pago](https://img.shields.io/badge/Mercado_Pago-SDK-00B1EA?style=flat&logo=mercadopago&logoColor=white)](https://www.mercadopago.com/)
[![JWT](https://img.shields.io/badge/Security-JWT-black?style=flat&logo=jsonwebtokens&logoColor=white)](https://jwt.io/)
[![Cloudinary](https://img.shields.io/badge/CDN-Cloudinary-3448C5?style=flat&logo=cloudinary&logoColor=white)](https://cloudinary.com/)

Thrill API es el motor transaccional (backend) de una plataforma de e-commerce moderna. Expone una arquitectura RESTful segura y escalable, diseñada para la gestión dinámica de catálogos, autenticación descentralizada de usuarios y el procesamiento integral de pagos y órdenes.

---

## 🚀 Mi Rol y Contribuciones Destacadas

Este proyecto fue desarrollado bajo un modelo colaborativo. Mi enfoque principal (`MaxonCoreDev`) radicó en la ingeniería de la **Lógica de Dominio y las Integraciones de Terceros (Third-party APIs)**. 

Mis responsabilidades y aportes técnicos en este repositorio incluyen:

* **Orquestación de Pagos (Mercado Pago):** Desarrollo del `PagoController` e integración del SDK de Mercado Pago. Implementé la generación de preferencias de pago dinámicas y el procesamiento seguro de transacciones.
* **Motor Transaccional de Órdenes:** Autoría de la lógica de negocio en `OrdenCompraService`. Diseñé el flujo completo de *checkout*, incluyendo validación de stock atómico (`ProductoTalle`), aplicación de reglas de descuentos y persistencia de estados de la orden.
* **Modelado de Catálogo Dinámico:** Desarrollo de `ProductoServiceImpl`, estableciendo una estructura robusta para manejar productos con variantes múltiples (talles, tipos, categorías) y su ciclo de vida dentro de la plataforma.

---

## 🏗️ Arquitectura y Flujo del Sistema

La aplicación está construida sobre una arquitectura en capas (MVC) que respeta los principios SOLID de Spring Boot:

1. **Gestión de Identidad Stateless (JWT):** Implementación de filtros en Spring Security para la validación de firmas de JSON Web Tokens (`jjwt`), garantizando autenticación y autorización sin estado en cada petición.
2. **Capa de Exposición (Controladores):** Endpoints RESTful estandarizados y documentados (Swagger/OpenAPI) para el consumo asíncrono del cliente.
3. **Capa de Servicios:** Aislamiento de las reglas de negocio complejas, asegurando que los controladores se limiten estrictamente al enrutamiento HTTP.
4. **Persistencia y Delivery de Assets:** Uso de Spring Data JPA (Hibernate) para el mapeo objeto-relacional en **MySQL**. Los assets multimedia son externalizados a **Cloudinary** (CDN), optimizando el ancho de banda y los tiempos de carga (latency).

### Flujo de Checkout
`Cliente -> Interceptor JWT -> Controlador -> Validación Atómica de Stock -> API Mercado Pago (Preferencia) -> Persistencia MySQL (Estado: Pendiente) -> Retorno de Gateway URL`.

---

## 👥 Equipo de Ingeniería y Atribuciones

Este sistema es el resultado de un esfuerzo conjunto, dividiendo las responsabilidades arquitectónicas para emular flujos de trabajo de la industria. Extiendo mi reconocimiento a mis colegas:

* 💻 **Máximo Ceverino** - *Lógica de Dominio, Gestión de Catálogo e Integraciones de Pago.*
* 🛡️ **[OriTechCode](https://github.com/OriTechCode)** - *Arquitectura Base, Módulo de Seguridad (Auth JWT) e Infraestructura de Datos.*
* 🌐 **[MaximoAF](https://github.com/MaximoAF)** - *Integración Frontend-Backend, Políticas de CORS y Estrategia de Despliegue.*

---

## 🛠️ Stack Tecnológico

* **Framework Base:** Java 17, Spring Boot 3.4.4
* **Persistencia:** MySQL (mysql-connector-java), Spring Data JPA
* **Seguridad:** Spring Security, JSON Web Tokens (JWT)
* **Integraciones:** MercadoPago SDK Java, Cloudinary HTTP44
* **Herramientas:** Maven, Lombok, Swagger/OpenAPI

---

## ⚙️ Despliegue Local

> **Prerrequisitos:** Entorno Java (JDK 17+), instancia de MySQL y Maven.

1. **Clonar Repositorio:**
   ```bash
   git clone [https://github.com/tu-usuario/thrill-ecommerce-api.git](https://github.com/tu-usuario/thrill-ecommerce-api.git)
   cd thrill-ecommerce-api
   ```

2. **Variables de Entorno:**
   Configura el esquema en MySQL y provee las credenciales en `src/main/resources/application.properties` (o vía variables de entorno en tu IDE):
   * Base de Datos (`spring.datasource.username`, `spring.datasource.password`).
   * CDN (`cloudinary.url`).
   * Pasarela de Pago (`mercadopago.access-token`).
   * Firma Criptográfica (`jwt.secret`).

3. **Compilación y Ejecución:**
   ```bash
   ./mvnw spring-boot:run
   ```
4. **Exploración de la API:**
   Accede a la interfaz de Swagger UI en: `http://localhost:8080/swagger-ui.html`
