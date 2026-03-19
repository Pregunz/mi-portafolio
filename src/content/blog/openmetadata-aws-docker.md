---
title: 'Lo que aprendí operando OpenMetadata en AWS'
description: 'Mi experiencia dando soporte a la plataforma OpenMetadata desplegada en AWS sobre Docker: qué reviso, qué falla y cómo se resuelve.'
pubDate: '2026-02-01'
---

Desde febrero de 2026 estoy dando soporte a OpenMetadata en producción para un cliente en AWS. No fui el que lo desplegó desde cero — llegué a un entorno ya funcionando y mi rol es mantenerlo estable. Esto es lo que he aprendido en el camino.

## ¿Qué es OpenMetadata?

Es una plataforma open source de catalogación y gobernanza de datos. Básicamente permite a las empresas documentar y entender qué datos tienen, de dónde vienen y cómo se mueven.

El entorno corre sobre contenedores Docker en AWS, con estos servicios principales:

- **OpenMetadata Server** — API y UI
- **MySQL** — base de datos de metadatos
- **Airflow** — orquestador de ingestas
- **Elasticsearch** — índice de búsqueda

## Qué reviso en el día a día

Lo primero siempre es verificar que todos los contenedores estén corriendo. Si alguno aparece con problemas, hay que revisar los logs de ese servicio específico para entender qué pasó.

Los errores más frecuentes que he visto son timeouts de conexión con MySQL o Airflow, y problemas de autenticación en conectores de ingesta.

## Qué pasa cuando una ingesta falla

Cuando un pipeline de ingesta falla, lo primero es verificar conectividad entre el contenedor y la fuente de datos. Si hay conectividad pero igual falla, se revisan los parámetros de configuración en el conector — principalmente timeouts y credenciales.

## El entorno no es genérico

OpenMetadata tiene una instalación base estándar — pero lo que corre en Hortifruit está configurado según su arquitectura, sus fuentes de datos y sus necesidades específicas. Llegar a ese entorno y entender qué estaba personalizado, qué conectores estaban activos y cómo fluía la ingesta de datos fue el primer trabajo real antes de poder dar soporte con criterio.

## Lo que más me ha costado entender

La parte más compleja no es el troubleshooting técnico sino entender el flujo completo: por qué falló una ingesta específica requiere conocer tanto el conector, como la fuente de datos, como el scheduler de Airflow. Todo está conectado.

## Documentación

Cada incidencia queda registrada con causa raíz y solución. Eso alimenta el informe mensual al cliente y sirve para no repetir el mismo diagnóstico dos veces.

---

*Escrito desde mi experiencia como Consultor Asistente en el proyecto Hortifruit, desde febrero 2026.*
