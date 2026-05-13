# 🚪 API Gateway - Sistema de Gestión de Mascotas

Este repositorio contiene el **API Gateway** principal del ecosistema, desarrollado con **Spring Cloud Gateway**. Actúa como el punto de entrada único (Single Entry Point) para todo el tráfico externo que se dirige hacia los microservicios de negocio, gestionando el enrutamiento dinámico, el filtrado de seguridad y el balanceo de carga.

## 🚀 Arquitectura y Prácticas DevOps

Como componente crítico de infraestructura, el API Gateway desacopla a los clientes de la ubicación real de los microservicios. Esto permite realizar cambios en la red interna (como mover servicios de instancia o escalar horizontalmente) sin afectar al consumidor externo.

El despliegue está 100% automatizado mediante un pipeline de **CI/CD** en GitHub Actions:
1. Compila el binario Java utilizando Maven/Gradle.
2. Genera una imagen Docker optimizada.
3. Empuja la imagen al registro de **Amazon ECR**.
4. Despliega de forma desatendida en la instancia **EC2** correspondiente mediante comandos de **AWS Systems Manager (SSM)**, inyectando dinámicamente las configuraciones de red de AWS.

### 🌐 Ecosistema de Infraestructura en AWS
El API Gateway se encuentra en la frontera del ecosistema, compartiendo nodo con la capa de presentación:

* **Nodo Web:** **ApiGateway** (Este repositorio) 📍 y Frontend
* **Nodo Back 1:** Eureka Server y BFF
* **Nodo Back 2:** Microservicios de Mascotas y Usuarios
* **Nodo Back 3:** Microservicios de Geolocalización y Notificaciones
* **Nodo Back 4:** Motor de Coincidencias
* **Base de Datos:** SanosDB (PostgreSQL)

## 🛠️ Tecnologías Principales

* **Framework:** Java 17 / Spring Boot 3
* **Gateway Engine:** Spring Cloud Gateway (Non-blocking API)
* **Cloud Native:** Netflix Eureka Client (Service Discovery)
* **Contenedores:** Docker
* **CI/CD:** GitHub Actions
* **Infraestructura AWS:** EC2, ECR, SSM, IAM

## ⚙️ Enrutamiento Dinámico y Resiliencia

El Gateway no utiliza rutas estáticas; en su lugar, está integrado con **Eureka**. 

* **Service Discovery Routing:** Al recibir una petición, el Gateway consulta al servidor Eureka para resolver el nombre del servicio (ej. `MS-GEOLOCALIZACION`) a una IP privada de AWS.
* **Load Balancing:** Distribuye el tráfico de forma inteligente entre las instancias disponibles registradas en Eureka.
* **Seguridad:** Centraliza la validación de peticiones antes de que estas penetren en la red interna de microservicios.

## 📦 Repositorios del Proyecto

Explora el resto de la infraestructura y microservicios de este ecosistema:

**Frontend y Puertas de Enlace**
* 🌐 [Frontend_eft_fullstack_III](https://github.com/NBello26/Frontend_eft_fullstack_III)
* 🚪 [ApiGateway_eft_fullstack_III](https://github.com/NBello26/ApiGateway_eft_fullstack_III) *(Estás aquí)*
* 🌉 [BFF_eft_fullstack_III](https://github.com/NBello26/BFF_eft_fullstack_III)

**Descubrimiento y Base de Datos**
* 🧭 [Eureka_eft_fullstack_III](https://github.com/NBello26/Eureka_eft_fullstack_III)
* 🗄️ [BD_eft_fullstack_III](https://github.com/NBello26/BD_eft_fullstack_III)

**Microservicios de Negocio**
* 🐾 [Reporte_Mascota_eft_fullstack_III](https://github.com/NBello26/Reporte_Mascota_eft_fullstack_III)
* 👤 [Usuarios_eft_fullstack_III](https://github.com/NBello26/Usuarios_eft_fullstack_III)
* 📍 [Geolocalizacion_eft_fullstack_III](https://github.com/NBello26/Geolocalizacion_eft_fullstack_III)
* 🔔 [Notificaciones_eft_fullstack_III](https://github.com/NBello26/Notificaciones_eft_fullstack_III)
* 🧩 [Coincidencias_eft_fullstack_III](https://github.com/NBello26/Coincidencias_eft_fullstack_III)

---
*Desarrollado como parte del proyecto final de integración de arquitectura DevOps.*
