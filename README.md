# 🚀 FivePeaks CRM - Backend API

Este repositorio contiene el servidor Backend (Cerebro) del CRM de FivePeaks. Está construido con Node.js y Express, y se encarga de gestionar de forma segura la lógica de negocio, la autenticación de usuarios y la conexión directa con la base de datos de Firebase.

## 🏗️ Arquitectura del Sistema

Este proyecto utiliza una arquitectura de 3 capas (Frontend, Backend, Base de Datos) para garantizar la máxima seguridad y escalabilidad.

```mermaid
graph TD
    Usuario((👤 Usuario / Comisionista))
    
    subgraph Frontend [El Rostro - Frontend]
        GitHub[🌐 GitHub Pages]
        Login[🔑 Login de Google]
    end

    subgraph Backend [El Cerebro - Backend]
        Render[🚀 Servidor en Render]
        Verificador[🛡️ Capa de Seguridad]
        Servicios[⚙️ Lógica de Leads]
    end

    subgraph DB [La Memoria - Base de Datos]
        Firestore[(🔥 Firebase Firestore)]
    end

    Usuario -->|1. Entra a la web| GitHub
    GitHub -->|2. Inicia sesion| Login
    GitHub -->|3. Peticiones HTTP| Render
    Render -->|4. Verifica VIP| Verificador
    Render -->|5. Procesa datos| Servicios
    Servicios <-->|6. Lee y Guarda| Firestore
