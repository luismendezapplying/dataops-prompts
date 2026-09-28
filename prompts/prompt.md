# Prompt: Lectura incremental por `ingestion_id`

## Contexto
Los jobs genéricos de Glue `staging_to_raw_vault` leen completas las tablas fuente de staging en cada ejecución, reprocesando datos de ingestas anteriores.

## Objetivo
Pasar a lectura incremental, filtrada por `ingestion_id`, en los jobs genéricos de la cadena landing → raw → staging → raw_vault.

## Cambios que ya tengo contemplados
1. Agregar el parámetro `ingestion_id` a los jobs genéricos `landing_to_raw` y `raw_to_staging`. El valor lo provisiona MWAA.
2. Agregar la columna de metadata `ingestion_id` a las tablas de raw y staging.
3. Filtrar la lectura en los jobs para no reprocesar datos de ingestas anteriores.

## Lo que necesito de ti
1. Verifica si mis cambios son suficientes y correctos. Identifica qué cambios específicos faltan (por ejemplo: `staging_to_raw_vault` también debe recibir `ingestion_id`, DAGs de MWAA, DDL/evolución de esquema en Iceberg, backfill de registros existentes, idempotencia y reintentos, manejo de reprocesos).
2. Propón otros cambios o riesgos que no haya considerado.
3. Define cómo validar rápidamente con pruebas de carga usando `sunat_diario` (por ejemplo: dos ingestas consecutivas y verificación de que la segunda solo procesa los datos nuevos).
4. Genera un **execution plan** paso a paso, ordenado por dependencias, con criterios de validación por paso y estrategia de rollback.

## Formato de salida
- Primero: lista de cambios adicionales y riesgos.
- Después: execution plan numerado.
- Conciso; sin explicaciones teóricas.