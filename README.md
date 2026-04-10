# 🚀 FivePeaks CRM - Backend API

Este repositorio contiene el servidor Backend (Cerebro) del CRM de FivePeaks. Está construido con Node.js y Express, y se encarga de gestionar de forma segura la lógica de negocio, la autenticación de usuarios y la conexión directa con la base de datos de Firebase.

## 🏗️ Arquitectura del Sistema

Este proyecto utiliza una arquitectura de 3 capas (Frontend, Backend, Base de Datos) para garantizar la máxima seguridad y escalabilidad.

```mermaid
graph TD
    Usuario((👤 Usuario /<br>Comisionista))
    
    subgraph &quot;El Rostro (Frontend)&quot;
        GitHub[🌐 GitHub Pages<br>index.html / CSS / JS]
        Login[🔑 Login de Google<br>Firebase Auth]
    end

    subgraph &quot;El Cerebro (Backend)&quot;
        Render[🚀 Servidor en Render<br>Node.js + Express]
        Verificador[🛡️ Capa de Seguridad<br>/api/auth/verify]
        Servicios[⚙️ Capa de Servicios<br>Lógica de Leads y Socios]
    end

    subgraph &quot;La Memoria (Base de Datos)&quot;
        Firestore[(🔥 Firebase Firestore)]
        Col_Users[Colección:<br>usuarios_autorizados]
        Col_Datos[Colecciones:<br>leads y comisionistas]
    end

    Usuario --&gt;|1. Entra a la URL publica| GitHub
    GitHub --&gt;|2. Inicia sesion| Login
    GitHub --&gt;|3. Peticiones HTTP mediante fetch| Render
    
    Render --&gt; Verificador
    Verificador --&gt;|Consulta si el email es VIP| Col_Users
    
    Render --&gt; Servicios
    Servicios &lt;--&gt;|Lee, Crea, Edita, Borra| Col_Datos

    style Usuario fill:#f9f9f9,stroke:#333,stroke-width:2px
    style GitHub fill:#e1f5fe,stroke:#0288d1,stroke-width:2px
    style Render fill:#e8f5e9,stroke:#388e3c,stroke-width:2px
    style Firestore fill:#fff3e0,stroke:#f57c00,stroke-width:2px
    style Login fill:#ffe0b2,stroke:#f57c00,stroke-width:1px
    style Verificador fill:#c8e6c9,stroke:#388e3c,stroke-width:1px
    style Servicios fill:#c8e6c9,stroke:#388e3c,stroke-width:1px
