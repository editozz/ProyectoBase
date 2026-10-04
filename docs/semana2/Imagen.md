# Diagrama de conexión — Interfaz, Lógica y Stellar

```mermaid
flowchart TB
    subgraph USUARIO["Usuario"]
        A1[Coordinador académico]
        A2[Secretario académico]
        A3[Estudiante]
        A4[Institución receptora / Empleador]
    end

    subgraph INTERFAZ["Capa de Interfaz (Frontend)"]
        B1[Panel institucional<br/>Registro de créditos]
        B2[Panel del estudiante<br/>Consulta y compartición]
        B3[Verificador público<br/>Consulta de autenticidad]
    end

    subgraph LOGICA["Capa de Lógica (Backend)"]
        C1[API de registro<br/>Valida y formatea créditos]
        C2[Servicio de firma<br/>Firma con llave institucional]
        C3[Servicio de verificación<br/>Consulta y valida]
        C4[Base de datos local<br/>Caché y metadatos]
    end

    subgraph STELLAR["Red Stellar"]
        D1[Cuenta institucional<br/>Stellar Keypair]
        D2[Transacción<br/>Registro del crédito]
        D3[Ledger<br/>Histórico inmutable]
        D4[Horizon API<br/>Consulta pública]
    end

    A1 --> B1
    A2 --> B1
    A3 --> B2
    A4 --> B3

    B1 --> C1
    B2 --> C3
    B3 --> C3

    C1 --> C2
    C2 --> D1
    D1 --> D2
    D2 --> D3
    D3 --> D4

    C3 --> D4
    C4 -.-> C1
    C4 -.-> C3
```

## Tabla de capas

| Capa | Componente | Qué hace |
| :---: | --- | --- |
| **Interfaz** | Panel institucional | Registra créditos aprobados |
| **Interfaz** | Panel del estudiante | Consulta y comparte trayectoria |
| **Interfaz** | Verificador público | Confirma autenticidad sin contactar a la institución |
| **Lógica** | Servicio de firma | Firma créditos con llave institucional |
| **Lógica** | Servicio de verificación | Consulta el ledger para validar |
| **Stellar** | Ledger | Histórico inmutable de créditos |
| **Stellar** | Horizon API | Consulta pública para verificadores |