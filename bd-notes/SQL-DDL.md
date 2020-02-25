# DDL (Data Definition Language)

**Este sublenguaje de SQL nos permite definir las características u objetos de una BBDD. Sus principales cláusulas son:**

Cláusula | Acción
--- | ---
**`CREATE`** | Nos permite crear una BBDD, una tabla para una BBDD existente, un usuario o un esquema.
**`ALTER`** | Nos permite añadir, eliminar o modificar columnas de una tabla y también añadir o eliminar restricciones.
**`DROP`** | Elimina una tabla de una BBDD.
**`TRUNCATE`** | Elimina los datos de una tabla, pero no la tabla en sí.
**`RENAME`** | Nos permite renombrar una tabla.

## **`CREATE DATABASE | SCHEMA`**

### Fórmula CREATE DATABASE | SCHEMA

```SQL
CREATE (DATABASE | SCHEMA) [IF-NOT-EXISTS] nombreDB [CHARACTER SET NOMBRE_CHARSET] [COLLATE NOMBRE_REGLAS_COMPARACIÓN];
```

Ejemplo en MySQL:

```SQL
CREATE DATABASE myDatabase CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci;
```

- Con **`CHARACTER SET ...`** le indicamos la codificación de caracteres que vamos a utilizar. **'utf8mb4'** es la implementación de
UTF-8 utilizada en MySQL. Luego le indicamos qué reglas queremos utilizar para comparar los caracteres unos de otros con **'COLLATE'**.
**utf8mb4_0900_ai_ci** es la recomendación en MySQL.
- **[Declaración de la codificación en MySQL](https://dev.mysql.com/doc/refman/8.0/en/charset-database.html)**
- **[Codificaciones implementadas en MySQL](https://dev.mysql.com/doc/refman/8.0/en/charset-unicode-sets.html)**
- **[Relación CHARSET-COLLATE en MySQL](https://stackoverflow.com/questions/341273/what-does-character-set-and-collation-mean-exactly#341333)**

Ejemplo en PostgreSQL:

```SQL
CREATE DATABASE music2
    LC_COLLATE 'sv_SE.iso885915' LC_CTYPE 'sv_SE.iso885915' -- LC_CTYPE indica la clasificación de los caracteres utilizada en la BBDD
    ENCODING LATIN9
    TEMPLATE template0; -- Esqueleto de la BBDD utilizado en PostgreSQL
```

- **[Declaración de la codificación en PostgreSQL](https://www.postgresql.org/docs/12/sql-createdatabase.html)**
- **[Codificación en PostgreSQL](https://www.postgresql.org/docs/12/multibyte.html#MULTIBYTE-CHARSET-SUPPORTED)**
- **[Documentación de PostgreSQL](https://www.postgresql.org/files/documentation/pdf/12/postgresql-12-US.pdf)**

---

## **`CREATE TABLE`**

### Fórmula CREATE-TABLE

```SQL
CREATE TABLE nombreTabla (
primaryKeyName [Data type] PRIMARY KEY,
atribUno NCHAR(...),
atribDos NCHAR(...),
...
[CONSTRAINT ...]
);
```
