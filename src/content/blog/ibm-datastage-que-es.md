---
title: '3 años operando IBM DataStage: qué es y qué aprendí'
description: 'Una mirada honesta a IBM DataStage desde el rol de soporte y operaciones, no desde el diseño.'
pubDate: '2025-10-01'
---

Llevo más de 3 años dando soporte a IBM DataStage en producción para clientes como BCI, Claro y Duoc UC. No soy el que diseña los pipelines ETL — mi rol ha sido mantener la plataforma funcionando. Esto es lo que aprendí desde ese lugar.

## Qué es IBM DataStage

Es una herramienta ETL (Extract, Transform, Load) empresarial. Se usa en empresas grandes para mover y transformar datos entre sistemas — por ejemplo, extraer datos de una base Oracle, procesarlos y cargarlos en un data warehouse.

Forma parte de la suite **IBM InfoSphere Information Server**:

| Componente | Para qué sirve |
|------------|----------------|
| DataStage | Motor ETL principal |
| QualityStage | Limpieza y calidad de datos |
| Information Analyzer | Perfilado de datos |
| IBM DB2 | Base de datos subyacente |

## Versiones que he tocado

- **v8.7** — legacy, algunos clientes aún la usan
- **v11.5** — versión intermedia
- **v11.7** — la más estable, con soporte vigente
- **DataStage SaaS / Cloud Pak for Data** — versión en la nube de IBM

Cada versión tiene sus particularidades. Pasar de 8.7 a 11.7 no es trivial — el ambiente cambia bastante.

## Qué hago cuando algo falla

Lo primero siempre es revisar el estado de los jobs desde DataStage Director. Los estados que más importan:

- **Running** — ok
- **Failed** — revisar logs
- **Aborted** — algo crítico pasó

Los logs del engine en Linux tienen rutas específicas según el componente. Otro problema frecuente es el espacio en disco — DataStage genera datasets temporales que se acumulan y hay que monitorear y limpiar periódicamente.

## DataStage en la nube (Cloud Pak for Data)

La versión SaaS corre sobre Kubernetes. La diferencia operativa principal es que todo se maneja desde la web — no hay cliente de escritorio. Los incidentes se reportan directamente a IBM Support.

## La plataforma es la misma, el entorno no

IBM DataStage es el mismo producto en BCI, Claro y Duoc UC — pero cada uno lo tiene configurado según su infraestructura, sus jobs, sus fuentes de datos y sus procesos internos. Llegar a un entorno nuevo y entender rápido qué está personalizado y qué es estándar es una habilidad que se desarrolla con el tiempo y que marca la diferencia entre dar soporte con criterio o a ciegas.

## Lo más difícil del rol de soporte

Entender por qué falla un job requiere conocer la plataforma, la infraestructura subyacente y a veces el negocio del cliente. No siempre tienes toda esa información. Aprendes a diagnosticar con lo que tienes y a saber cuándo escalar.

---

*Escrito desde mi experiencia como Consultor Asistente en Factor IT, operando IBM DataStage para múltiples clientes desde 2023.*
