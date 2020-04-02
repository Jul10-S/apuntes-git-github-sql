# DDL (Data Definition Language)

**Este sublenguaje de SQL nos permite definir las características u objetos de una BBDD. Sus principales cláusulas son:**

Cláusula | Acción
--- | ---
**`CREATE`** | Nos permite crear una BBDD, una tabla para una BBDD existente, un usuario (en DCL) o un esquema.
**`ALTER`** | Nos permite añadir, eliminar o modificar columnas de una tabla y también añadir o eliminar restricciones.
**`DROP`** | Elimina una tabla de una BBDD.
**`TRUNCATE`** | Elimina los datos de una tabla, pero no la tabla en sí.
**`RENAME`** | Nos permite renombrar una tabla.

## **`CREATE DATABASE | SCHEMA`**

### Fórmula CREATE DATABASE | SCHEMA

```SQL
CREATE (DATABASE | SCHEMA) [IF-NOT-EXISTS] nombreDB [CHARACTER SET = NOMBRE_CHARSET] [COLLATE = NOMBRE_REGLAS_COMPARACIÓN];

-- En MariaDB existe la cláusula [OR REPLACE], que creará la BBDD si no existe y si existe eliminará la que está creada para crear una nueva.
```

Ejemplo en MariaDB:

```SQL
CREATE DATABASE My_Database CHARACTER SET = utf8mb4 COLLATE = utf8_spanish_ci;
```

- Crea la BBDD 'My_Database' siempre y cuando no exista.
- Con **`CHARACTER SET = ...`** le indicamos la codificación de caracteres que vamos a utilizar. **utf8mb4** es la implementación de
UTF-8 utilizada en MariaDB. Luego le indicamos qué reglas queremos utilizar para comparar los caracteres unos de otros con **`COLLATE`**.
**utf8_spanish_ci** es el utilizado para comparar caracteres en castellano.
- **[Creación de BBDD en MariaDB](https://mariadb.com/kb/en/create-database/)**
- **[Codificaciones implementadas en MariaDB](https://mariadb.com/kb/en/supported-character-sets-and-collations/)**
- **[Relación CHARSET-COLLATE](https://stackoverflow.com/questions/341273/what-does-character-set-and-collation-mean-exactly#341333)**

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
CREATE TABLE [IF-NOT-EXISTS] Nombre_Tabla (
<atributo1> [DOMINIO] [PRIMARY KEY],
<atributo2> [DOMINIO] [NOT NULL] [UNIQUE] ...,
<atributon> [DOMINIO] [NOT NULL] [UNIQUE] ...,
[CONSTRAINT ...] -- Restricciones
);
```

- **Para crear tablas empleamos la cláusula compuesta `CREATE TABLE`, seguida del nombre de la tabla.**
- **Una tabla se compone de columnas (atributos) y tuplas de información relacionada con los atributos. Para diferenciar las tuplas unas de otras**
**empleamos las claves primarias y éstas las podemos declarar con el identificador `PRIMARY KEY` después de la declaración del dominio o después de la declaración de atributos, a modo de restricción.**
- **Podemos emplear `NOT NULL` para indicar que no se permite la introducción de valores nulos en una columna en concreto.**
- **Empleamos `UNIQUE` para indicar que no queremos que se repitan los valores de una columna.**
- **Separamos los distintos atributos mediante comas.**
- **El bloque de código empleado para crear la tabla siempre tiene que acabar en ;.**

---

## **`CREATE DOMAIN`**

**Los dominios indican el tipo de datos que queremos emplear para un atributo. El tipo de datos condicionará los posibles valores que una columna podrá tomar.**
**Algunos de los tipos de datos existentes en MariaDB son los siguientes:**

NUMÉRICOS |
--------- |
**INT(M):** (INTEGER) número entero. Cuando está asignado va desde -2147483648 hasta 2147483647. Cuando no lo está va desde 0 hasta 4294967295. https://mariadb.com/kb/en/int/|
**BOOLEAN:** valores booleanos (verdadero o falso - true or false). 0 se considera falso y cualquier otro valor es verdadero. https://mariadb.com/kb/en/boolean/|
**BIGINT(M):** número entero largo. Cuando está asignado va desde -9223372036854775808 hasta 9223372036854775807. Cuando no lo está va desde 0 hasta 18446744073709551615. https://mariadb.com/kb/en/bigint/|
**DECIMAL(M[, D]):** valor decimal. Permite como máximo 65 dígitos en la parte entera y 38 en la mantisa. Si se especifica UNSIGNED no se permitirán los valores negativos. https://mariadb.com/kb/en/decimal/|
**FLOAT(M,D):** valores de coma flotante. Sus valores pueden ser desde -3.402823466E+38 hasta -1.175494351E-38, 0 y desde 1.175494351E-38 hasta 3.402823466E+38. https://mariadb.com/kb/en/float/|
**DOUBLE(M,D):** (valores de coma flotante de doble precisión. Sus valores pueden ser desde -1.7976931348623157E+308 hasta -2.2250738585072014E-308, 0 y desde 2.2250738585072014E-308 hasta 1.7976931348623157E+308. https://mariadb.com/kb/en/double/|

---

 CADENAS-CARACTERES|
 ------------------|
**STRING:** cadenas de caracteres. Pueden ir entre comillas simples o dobles y permiten las [secuencias de escape](./img/secuencias_escape.png). https://mariadb.com/kb/en/string-literals/|
**CHAR(M):** cadenas de caracteres de longitud fija: 0 a 255 caracteres. https://mariadb.com/kb/en/char/|
**VARCHAR(M):** cadenas de longitud variable. Permite cadenas desde 0 a 65532 caracteres. https://mariadb.com/kb/en/varchar/|
**MEDIUMTEXT:** cadenas de hasta 16,777,215 caracteres. https://mariadb.com/kb/en/mediumtext/|
**LONGTEXT:** cadenas de hasta 4,294,967,295 caracteres. https://mariadb.com/kb/en/longtext/|

---

FECHA-HORA|
----------|
**DATE:** fechas. Los valores siguen el formato "YYYY-MM-DD". https://mariadb.com/kb/en/date/|
**TIME:** horas, minutos y segundos. Permite especificar la hora siguiendo el formato "HH:MM:SS.ssssss". https://mariadb.com/kb/en/time/|
**DATETIME:** unión de los formatos para fecha y hora. Sigue el formato "YYYY-MM-DD HH:MM:SS.ffffff". https://mariadb.com/kb/en/datetime/|
**TIMESTAMP:** igual que DATETIME. Se suele utilizar para guardar un registro de las inserciones y actualizaciones de datos. https://mariadb.com/kb/en/timestamp/|

---

OTROS|
-----|
**NULL:** valor desconocido. No es un valor cero o vacío.|
**AUTO_INCREMENT:** cada vez que se introducen nuevos datos y al tener este dominio una columna en concreto, sus valores irán en aumento. Suele utilizarse para claves primarias. https://mariadb.com/kb/en/auto_increment/|

- **Hay que tener en cuenta que los tipos de datos pueden variar según el sistema gestor que empleemos.**
- **[Más información sobre tipos de datos](https://www.tutorialcup.com/dbms/datatypes-variables.htm)**
- **[Más información sobre tipos de datos en MariaDB](https://mariadb.com/kb/en/data-types/)**

---

**La manera más eficiente de controlar los dominios en las BBDD es declarándolos por adelantado y luego llamándolos desde las tablas. Ésto lo hacemos empleando la siguiente fórmula:**

```SQL
CREATE DOMAIN [NOMBRE_DOMINIO] [DOMINIO];
```

---

