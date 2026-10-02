# Ley 21.719 + Snowflake: Guia Completa de Cumplimiento

Entrenamiento paso a paso para implementar cumplimiento con la **Ley 21.719 de 13 de diciembre de 2024** (Proteccion de Datos Personales de Chile) usando recursos nativos de Snowflake. Cubre desde fundamentos legales hasta operacion completa con 9 modulos ejecutables.

---

## Que esta incluido

| Archivo | Descripcion |
|---------|-------------|
| `LEY21719_SNOW.html` | Guia interactiva con teoria, SQL ejecutable y sidebar navegable (dark mode) |
| `LEY21719_SNOW.sql` | SQL consolidado (1100+ lineas) para ejecucion directa en Snowsight |

## Modulos

| # | Modulo | Articulos Ley 21.719 | Recursos Snowflake |
|---|--------|----------------------|-------------------|
| 1 | Fundamentos de la Ley 21.719 | Arts. 1-3 | Vision general de la arquitectura |
| 2 | Gobernanza y RBAC | Arts. 14 quater, 14 sexies | Roles, grants, segregacion de funciones |
| 3 | Clasificacion de Datos | Arts. 2, 16 | `SYSTEM$CLASSIFY`, tags de sistema |
| 4 | Tags Personalizados | Arts. 3, 12-13 | Object tagging, herencia, bases legales |
| 5 | Enmascaramiento Dinamico | Arts. 14 bis, 3 | Masking policies, tag-based masking |
| 6 | Row Access Policies | Art. 3 (finalidad), Art. 14 bis | RAP, limitacion de finalidad |
| 7 | Projection Policies | Art. 3 (proporcionalidad), Art. 16 | Projection policies (FAIL/NULLIFY), proporcionalidad |
| 8 | Derechos del Titular (ARCO-P) | Arts. 4-8, 10 | Stored procedures, portabilidad, anonimizacion |
| 9 | Auditoria y Cumplimiento | Arts. 14 bis-ter, 34 bis-quater | ACCESS_HISTORY, alertas, reportes |

## Defensa en Profundidad

El entrenamiento implementa tres capas independientes de proteccion en la misma tabla:

```
Capa 1: Row Access Policy    -> filtra FILAS (quien ve cuales registros)
Capa 2: Projection Policy    -> bloquea COLUMNAS en el output (quien ve cuales campos)
Capa 3: Masking Policy        -> transforma VALORES visibles (como aparecen los datos)
```

## Pre-requisitos

- Snowflake Enterprise Edition (o superior)
- Role `ACCOUNTADMIN` o `SYSADMIN` para configuracion inicial
- Snowsight (interfaz web) para ejecucion interactiva

## Como usar

1. **Configure las variables** al inicio del archivo SQL:
   ```sql
   SET LEY21719_USER      = '<SU_USUARIO>';
   SET LEY21719_DPO_EMAIL = '<SU_EMAIL>';
   ```

2. **Ejecute secuencialmente** cada modulo en Snowsight (Modulo 2 antes de 3, etc.)

3. **O abra el HTML** (`LEY21719_SNOW.html`) en el navegador para la guia interactiva con teoria y SQL lado a lado

## Limpieza

Para eliminar todos los objetos creados por el entrenamiento:

```sql
USE ROLE ACCOUNTADMIN;
DROP DATABASE IF EXISTS LEY21719_GOVERNANCE;
DROP DATABASE IF EXISTS EMPRESA_DEMO_CL;
DROP WAREHOUSE IF EXISTS LEY21719_TRAINING_WH;
DROP ROLE IF EXISTS LEY21719_DELEGADO_DATOS;
DROP ROLE IF EXISTS LEY21719_PRIVACY_ADMIN;
DROP ROLE IF EXISTS LEY21719_DATA_STEWARD;
DROP ROLE IF EXISTS LEY21719_ANALYST;
DROP ROLE IF EXISTS RRHH_ANALYST;
DROP ROLE IF EXISTS MARKETING_ANALYST;
DROP ROLE IF EXISTS FINANZAS_ANALYST;
DROP NOTIFICATION INTEGRATION IF EXISTS LEY21719_NOTIFICATIONS;
```

## Licencia

[MIT](LICENSE)
