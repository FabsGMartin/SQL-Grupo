# Proyecto de Creación de Base de Datos Relacional
![header](./assets/header_readme.png)
## 👤 Participantes

- Miguel Jiménez De La Torre
- Juan Pablo Rizzi 
- Angel Gómez Alonso
- Fabian González Martín
- Rebeca Díaz-Montenegro Sánchez

## 🖥️ Introducción
El proyecto consiste en diseñar e implementar una base de datos en PostgreSQL. Se creará un modelo E/R para definir entidades, atributos y relaciones, que luego se convertirá en un modelo lógico con tablas, claves primarias y foráneas. Se realizará la normalización de datos para evitar redundancias y garantizar integridad, y finalmente se creará la base de datos y se alojará en un servidor accesible desde aplicaciones externas.

## 📄 Tareas que realizar

1. **Modelo Entidad-Relación (E/R)**: Diseñar un modelo E/R que represente la estructura de la base de datos normalizada. Definir las entidades, atributos y relaciones entre ellas.

2. **Modelo Lógico de la Base de Datos**: Con base en el modelo E/R, desarrollar un modelo lógico de la base de datos. Esto implica definir la estructura de las tablas y sus campos, así como las claves primarias y foráneas necesarias.

3. **Normalización de Datos**: Analizar los datos y realizar una normalización adecuada para eliminar la redundancia y garantizar la integridad de los datos.

4. **Creación de la Base de Datos**: Utilizando un sistema de gestión de bases de datos de PostgreSQL, crear la base de datos y las tablas necesarias según el modelo lógico. Crear las queries necesarias para crear las tablas e ingestar los datos. Habrá que alojar en algún servidor vuestras bases de datos para poder acceder desde aplicaciones de terceros.
Algún servicio gratis de postgreSQL:

## 📑 Modelo Entidad-Relación (E/R)

![modelo_er](./assets/diagrama_er.png)

## 📉 Modelo Lógico de la Base de Datos
![modelo_lógico](./assets/SQL%20Import%20(postgresql)%20(6).png)

### 1. Modalidad:
Tabla de modalidades de dictado (p. ej., presencial, online).

Columnas
- id (INT, PK, NOT NULL): identificador único de la modalidad.
- modalidad (VARCHAR, NOT NULL): nombre de la modalidad.

**Relaciones**Modalidad (1) — (N) Profesores: cada profesor está asociado a una modalidad.

### 2. Campus:

Tabla de sedes.

Columnas
- id (INT, PK, NOT NULL): identificador único del campus.
- campus (VARCHAR, NOT NULL): nombre de la sede (p. ej., Madrid, Valencia).

**Relaciones**

Campus (1) — (N) Bootcamps: un campus puede albergar múltiples bootcamps.

### 3. Promociones:
Tabla de cohortes o ediciones.

Columnas
- id (INT, PK, NOT NULL): identificador único de la promoción.
- promocion (VARCHAR, NOT NULL): nombre de la promoción/edición.

**Relaciones**

Promociones (1) — (N) Bootcamps: una promoción agrupa varios bootcamps.

## 4. Verticales:
Tabla de áreas/verticales académicas (Data, Full Stack, Ciber, etc.).

Columnas
- id (INT, PK, NOT NULL): identificador del vertical.
- vertical (VARCHAR, NOT NULL): nombre del vertical.

**Relaciones**

Verticales (1) — (N) Bootcamps: un vertical puede tener muchos bootcamps.

Verticales (1) — (N) Proyectos: cada proyecto pertenece a un vertical.
 
## 5. Roles_profesores:
Tabla de roles de docentes (Lead, TA, etc.).

Columnas
- id (INT, PK, NOT NULL): identificador del rol.
- rol (VARCHAR, NOT NULL): nombre del rol.

**Relaciones**

Roles_profesores (1) — (N) Profesores: cada profesor tiene un rol.

## 6. Proyectos
Propósito: tabla de proyectos académicos que realizarán los alumnos.

Columnas
- id (INT, PK, NOT NULL): identificador del proyecto.
- nombre (VARCHAR, NOT NULL): título del proyecto.
- vertical_id (INT, FK, NOT NULL → Verticales.id): vertical al que pertenece.

**Relaciones**

Verticales (1) — (N) Proyectos.

Proyectos (1) — (N) Calificaciones: un proyecto recibe múltiples calificaciones (una por alumno).
 
## 7. Bootcamps
Propósito: instancia concreta de formación (vertical + campus + promoción).

Columnas
- id (INT, PK, NOT NULL): identificador del bootcamp.
- promocion_id (INT, FK, NOT NULL → Promociones.id): promoción/cohorte.
- campus_id (INT, FK, NOT NULL → Campus.id): sede.
- vertical_id (INT, FK, NOT NULL → Verticales.id): vertical académico.

**Relaciones**

Promociones (1) — (N) Bootcamps.

Campus (1) — (N) Bootcamps.

Verticales (1) — (N) Bootcamps.

Bootcamps (1) — (N) Alumnos: un bootcamp tiene muchos alumnos.

Bootcamps (1) — (N) Profesores: un bootcamp tiene muchos profesores.
 
## 8. Alumnos:
Tabla de registro de estudiantes.

Columnas
- id (INT, PK, NOT NULL): identificador del alumno.
- nombre (VARCHAR, NOT NULL): nombre completo.
- email (VARCHAR, NOT NULL): correo del alumno (idealmente único).
- bootcamp_id (INT, FK, NOT NULL → Bootcamps.id): bootcamp al que asiste.
- fecha_comienzo (DATE): fecha de inicio del alumno.
- aula (INT): número de aula/grupo (si aplica).

**Relaciones**

Bootcamps (1) — (N) Alumnos.

Alumnos (1) — (N) Calificaciones: un alumno puede tener varias calificaciones (una por proyecto evaluado).
 
### 9. Profesores:
Tabla de registro de docentes y su asignación.

Columnas
- id (INT, PK, NOT NULL): identificador del profesor.
- nombre (VARCHAR, NOT NULL): nombre completo.
- rol_id (INT, FK, NOT NULL → Roles_profesores.id): rol del docente.
- bootcamp_id (INT, FK, NOT NULL → Bootcamps.id): bootcamp asignado.
- modalidad_id (INT, FK, NOT NULL → Modalidad.id): modalidad en la que dicta.

**Relaciones**

Bootcamps (1) — (N) Profesores.

Roles_profesores (1) — (N) Profesores.

Modalidad (1) — (N) Profesores.
 
### 10. Calificaciones:
Tabla de evaluaciones (nota) que vinculan alumno–proyecto.

Columnas
- id (INT, PK, NOT NULL): identificador de la calificación.
- alumno_id (INT, FK, NOT NULL → Alumnos.id): alumno evaluado.
- proyecto_id (INT, FK, NOT NULL → Proyectos.id): proyecto evaluado.
- calificacion (VARCHAR, NOT NULL): nota (Apto/ No Apto).

**Relaciones**

Alumnos (1) — (N) Calificaciones.

Proyectos (1) — (N) Calificaciones.


## 🛠️ Herramientas utilizadas

 - Render
 - PgAdmin4
 - postgreSQL
 - Python


