---
title: 'Administrando Microsoft 365 en múltiples organizaciones'
description: 'Qué implica administrar entornos M365 de distintas organizaciones al mismo tiempo — usuarios, licencias y soporte.'
pubDate: '2025-02-01'
---

En Factor IT administré entornos Microsoft 365 para tres organizaciones distintas de forma simultánea: casia.tech, ceibo.tech y factorit.com. Cada una con su propio tenant, sus propios usuarios y sus propias configuraciones. Esto es lo que aprendí.

## Qué es un tenant de M365

Un tenant es el entorno de Microsoft 365 de una organización. Es completamente independiente de otros tenants — usuarios, licencias, configuraciones y datos no se mezclan entre organizaciones.

Administrar tres tenants a la vez significa tener acceso de administrador en los tres y poder cambiar entre ellos según lo que se necesite.

## Tareas habituales de administración M365

**Gestión de usuarios y licencias:**
- Crear y eliminar cuentas de usuario
- Asignar licencias (Microsoft 365 Business, Teams, Exchange)
- Gestionar grupos de seguridad y grupos de distribución
- Restablecer contraseñas y configurar MFA

**Soporte en servicios:**
- **Outlook** — problemas de correo, configuración de buzones compartidos, reglas
- **Teams** — canales, permisos, reuniones, integraciones
- **SharePoint** — permisos de sitios, bibliotecas de documentos
- **OneDrive** — sincronización, permisos, recuperación de archivos

**Administración general:**
- Monitorear el estado de los servicios desde el centro de administración
- Revisar alertas y notificaciones de Microsoft
- Aplicar políticas de seguridad y cumplimiento

## Lo particular de administrar múltiples tenants

El principal desafío es no confundirse entre organizaciones. Una acción en el tenant equivocado puede afectar a usuarios que no corresponde.

La disciplina es simple: siempre verificar en qué tenant estás antes de hacer cualquier cambio. Y documentar cada acción con la organización afectada.

## Cada organización tiene su propia configuración

M365 es el mismo producto en los tres tenants — pero cada organización lo tiene configurado distinto. Licencias distintas, políticas distintas, flujos de trabajo distintos. Lo que funciona en un tenant no necesariamente aplica en otro. Entender esas diferencias antes de hacer cualquier cambio es lo que evita afectar a usuarios que no corresponde.

## Lo que aprendí

M365 tiene una cantidad enorme de configuraciones posibles. La clave no es conocerlas todas — es saber dónde buscar cuando aparece algo nuevo. El centro de administración de Microsoft y la documentación oficial son las herramientas más útiles.

---

*Basado en mi experiencia administrando entornos M365 en Factor IT, febrero 2025.*
