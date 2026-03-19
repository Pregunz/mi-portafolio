---
title: 'Implementando IBM Information Server 11.7 desde cero'
description: 'Mi experiencia participando en la implementación completa de IBM IIS 11.7 en Porvenir Pensiones — instalación, configuración, coordinación y entrega.'
pubDate: '2024-06-01'
---

El proyecto de Porvenir fue distinto a los demás. En la mayoría de mis proyectos llego a un entorno ya instalado y mi rol es mantenerlo. En Porvenir participé en la implementación desde cero: preparación, instalación, configuración y entrega. Eso cambia completamente cómo entiendes la plataforma después.

## Qué implica implementar IBM IIS desde cero

IBM Information Server 11.7 es una suite con múltiples componentes que deben instalarse en orden:

- **Services tier** — servicios centrales de la plataforma
- **Engine tier** — motor de ejecución de DataStage
- **Client tier** — herramientas de escritorio (Designer, Director, Administrator)
- **Repository** — base de datos DB2 con metadatos y proyectos

Cada tier puede estar en servidores distintos o en el mismo, según el diseño del cliente.

## Lo más crítico: la preparación previa en RHEL

IBM IIS 11.7 corre principalmente sobre Red Hat Enterprise Linux (RHEL). Antes de ejecutar el instalador, el sistema operativo tiene que cumplir una lista de requisitos específicos. Si algo falla aquí, el instalador puede fallar o el sistema puede quedar inestable después.

Lo que se verifica antes de instalar:

- **Versión del SO** — debe estar en la matriz de compatibilidad de IBM
- **Espacio en disco** — IIS necesita espacio considerable en los directorios de instalación
- **Memoria RAM** — hay mínimos recomendados según la topología
- **Paquetes del sistema** — IBM IIS requiere librerías específicas instaladas en RHEL
- **Parámetros del kernel** — memoria compartida, semáforos y límites de archivos abiertos deben ajustarse según los valores mínimos que publica IBM en su documentación oficial
- **Límites del sistema** — el usuario administrador de DataStage necesita límites específicos de procesos y archivos
- **Usuario y grupo de DataStage** — el engine corre bajo un usuario dedicado que debe existir antes de instalar
- **SELinux** — en producción se coordina con el equipo de seguridad del cliente, ya que puede bloquear procesos si no está configurado correctamente
- **Hostname** — debe estar correctamente configurado y resolver en DNS

Esta coordinación con el equipo de infraestructura del cliente es clave — permisos de red, puertos abiertos, usuarios del sistema — todo depende de ellos.

## Qué hacer cuando algo falla durante la instalación

IBM IIS genera logs en distintas rutas según el componente que falló. Saber dónde mirar es parte del trabajo. Los problemas más frecuentes son de prerequisitos incompletos, permisos mal configurados o conectividad de red. Cada uno tiene síntomas distintos en los logs.

## La instalación estándar no existe

IBM publica una guía de instalación — pero cada implementación termina siendo distinta. En Porvenir había requisitos específicos de infraestructura, restricciones de red propias del cliente y configuraciones que se adaptaron sobre la marcha según lo que el entorno real permitía. La capacidad de leer esa situación y ajustar sin perder el hilo del proceso es lo que hace que una implementación llegue a buen término.

## Validación post-instalación

Una implementación no termina cuando el instalador dice "éxito". Hay que validar:

- Que todos los servicios levantan correctamente
- Que DataStage Designer se conecta al servidor
- Que hay conectividad con las fuentes de datos del cliente
- Que los jobs de prueba compilan y corren
- Que el entorno sobrevive un reinicio completo

Si pasa todo eso, el entorno está listo para entrega.

## Lo que me dejó este proyecto

Haber estado en la implementación desde el inicio me dio algo que el soporte diario no da: entender el entorno desde adentro. En soporte llegas a un entorno ya armado y aprendes sus particularidades. En una implementación entiendes por qué está armado así — las decisiones de diseño, los prerequisitos, las dependencias.

Lo más concreto que me llevé: el orden de validación post-instalación. Después de Porvenir tengo claro qué verificar cuando un entorno se arma o se migra, no solo cuando falla. Eso lo apliqué directamente en proyectos posteriores.

Y una lección general: dedica el doble de tiempo que crees necesario a la preparación del SO. La instalación en sí es guiada — lo que falla casi siempre es lo previo.

---

*Basado en mi participación en el proyecto Porvenir Pensiones y Cesantías, ago 2023 – dic 2024.*
