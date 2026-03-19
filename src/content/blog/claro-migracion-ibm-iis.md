---
title: 'Migración de IBM Information Server 8.7 y 11.5 a 11.7 en Claro'
description: 'Lo que aprendí durante años de soporte multiversión en Claro, incluyendo la migración de entornos IBM IIS a versión 11.7.'
pubDate: '2025-08-01'
---

En Claro di soporte a IBM Information Server en tres versiones distintas al mismo tiempo: 8.7, 11.5 y 11.7. Cada una en su propio entorno, con sus propias particularidades. Eventualmente el objetivo fue migrar hacia 11.7. Esto es lo que aprendí en ese proceso.

## Por qué coexistían tres versiones

No es raro en empresas grandes. Los sistemas ETL llevan años en producción y migrar todo de golpe es demasiado riesgo. Claro mantenía los entornos legacy funcionando mientras gradualmente se consolidaba en 11.7.

Eso significa que quien da soporte tiene que conocer las diferencias entre versiones — lo que funciona en 11.7 no necesariamente aplica igual en 8.7.

## Las diferencias más importantes entre versiones

**8.7** es la más antigua. Instalación en sistemas operativos más viejos, interfaz de administración distinta, y algunos comportamientos del engine que en versiones nuevas ya no existen. Los logs están en rutas distintas y la gestión de usuarios es diferente.

**11.5** es intermedia. Ya incorpora mejoras en rendimiento y la interfaz de administración es más similar a 11.7. Pero hay componentes que cambiaron de nombre o de ruta entre versiones.

**11.7** es la versión con soporte vigente. Arquitectura más estable, mejor integración con herramientas modernas y parches activos de IBM.

## Qué implica migrar de 8.7 o 11.5 a 11.7

Una migración de IBM IIS no es solo instalar la versión nueva. Implica:

- Validar compatibilidad del sistema operativo con 11.7
- Exportar los proyectos y jobs de DataStage desde la versión origen
- Instalar y configurar el nuevo entorno 11.7
- Importar los proyectos y validar que los jobs compilen y corran igual
- Verificar conectividad con todas las fuentes de datos
- Ejecutar pruebas en ambiente pre-productivo antes de pasar a producción

El paso más delicado es la validación de jobs — hay cambios de comportamiento entre versiones que pueden hacer que un job que corría bien en 8.7 falle en 11.7 aunque compile sin errores.

## Cada entorno es distinto aunque la plataforma sea la misma

IBM IIS 11.7 es el mismo producto en todos los clientes — pero cómo está instalado, configurado y usado varía completamente. En Claro había decisiones de arquitectura específicas, configuraciones personalizadas y procesos adaptados a su infraestructura. Llegar y entender qué estaba predeterminado y qué había sido modificado según sus necesidades fue parte del trabajo desde el primer día.

## Lo que más cuesta en soporte multiversión

Saber en qué versión estás en cada momento. Parece obvio, pero cuando atiendes incidentes de varios entornos al mismo tiempo, los comandos, rutas y comportamientos son distintos. La documentación interna es clave para no confundirlos.

---

*Basado en mi experiencia como Consultor Asistente en el proyecto Claro, desde abril 2023.*
