---
title: 'Instalando un cluster Power BI Gateway con alta disponibilidad'
description: 'Cómo participé en la instalación y migración de un cluster On-premises Data Gateway en modo Activo-Activo para Power BI Service en Duoc UC.'
pubDate: '2025-11-01'
---

Entre noviembre 2025 y febrero 2026 participé en la instalación de un cluster On-premises Data Gateway con alta disponibilidad para Power BI Service en Duoc UC. Acá explico qué hicimos y por qué.

## El problema que resolvíamos

Duoc UC usaba un solo gateway para conectar Power BI Service con sus fuentes de datos locales. Si ese servidor tenía problemas, todos los reportes que dependían de datos internos dejaban de actualizarse. Un punto único de falla en producción es inaceptable.

La solución fue instalar un cluster Activo-Activo con dos nodos:

| Servidor | Rol |
|----------|-----|
| WSPBI01 | Nodo primario |
| WSPBI02 | Nodo secundario |

Con ambos activos, Power BI distribuye las solicitudes entre los dos. Si uno cae, el otro sigue funcionando solo.

## Cómo se instala

### Nodo primario (WSPBI01)

1. Descargar el instalador de On-premises Data Gateway desde Power BI Service
2. Iniciar sesión con la cuenta de servicio
3. Crear el cluster con un nombre y guardar la **clave de recuperación** — esto es crítico

### Nodo secundario (WSPBI02)

1. Instalar el gateway igual que el primario
2. En la configuración, seleccionar **"Agregar a cluster existente"**
3. Ingresar la clave de recuperación del nodo primario

Listo. En **Configuración > Administrar gateways** de Power BI Service deben aparecer ambos nodos en estado **En línea**.

## Migración de datasets

Los datasets que apuntaban al gateway anterior hay que redirigirlos al nuevo cluster. Esto se hace desde la configuración de cada dataset en Power BI Service — seleccionas el nuevo cluster y mapeas las credenciales de cada fuente.

Después ejecutas una actualización manual para confirmar que todo funciona.

## Prueba de failover

La validación más importante: apagar el servicio de gateway en WSPBI01 y verificar que Power BI sigue actualizando usando WSPBI02. Si funciona, el cluster está bien configurado.

## Lo que no viene en el manual

La instalación del gateway sigue pasos estándar — pero la configuración real depende de la infraestructura del cliente. En Duoc UC había fuentes de datos internas con sus propias credenciales, reglas de red específicas y procesos de validación propios. Entender ese contexto antes de instalar es lo que permite hacer una migración sin interrumpir los reportes en producción.

## Lo que aprendí

Antes de este proyecto no había trabajado con Power BI Gateway. Lo que más me llevó tiempo fue entender el concepto de cluster en este contexto — no es como un cluster de servidores tradicional, es Power BI el que maneja el balanceo de carga automáticamente.

---

*Basado en el proyecto de Duoc UC, nov 2025 – feb 2026.*
