# CREAR UNA TABLA EN SQL

## ++++ Sintaxis sql estandar ++++

### -- Ejemplo 1 . Crear Tabla --
CREATE TABLE ARITISTA (
    clave_artista number(10,0),
    nombre_artista varchar (50),
    RFC varchar(13),
    clasificacion char(1)
    
);

### ---Ejemplo 2. Modificar la tabla ---
ALTER TABLE ARTISTA ADD (CURP varchar(13));
ALTER TABLE ARTISTA modify(CURP varchar(18));


### ---Ejercicio 3. Eleminar la columna CURP---
ALTER TABLE ARTISTA DROP COLUMN CURP;


### ---Ejercicio 4.Cambiar el nombre de clasificacion a clasificarlo ---
ALTER TABLE ARTISTA RENAME COLUMN clasificacion to clasificado;


### ---Ejercicio 5. Eliminar una tabla ---
DROP TABLE ARTISTA CASCADE CONSTRAINTS;



### ---Tabla con Constraints (restricciones)---
---A nivel columna ---
CREATE TABLE PROPIETARIO(
    propietario_id number(10,0) CONSTRAINT ppropietario_pk primary key,
    rfc varchar(13) not null CONSTRAINT propietario_rfc_uk unique,
    curp varchar(40) null CONSTRAINT propietario_curp_uk unique,
    nombre varchar(40) not null,
    ap_paterno varchar(40) not null,
    ap_materno varchar(40) not null,
    permiso_licencia char(1) not null,
    email varchar(40) not null,
    
);
--- Elimino mi tabla ---
DROP TABLE PROPIETARIO CASCADE CONSTRAINTS;

--- Tabla con restricciones a nivel columna ---
CREATE TABLE PROPIETARIO(
    propietario_id number(10,0),
    rfc varchar(13),
    curp varchar(40),
    nombre varchar(40) not null,
    ap_paterno varchar(40) not null,
    ap_materno varchar(40) not null,
    permiso_licencia char(1) not null,
    email varchar(40) not null,
    CONSTRAINT propietario_pk PRIMARY KEY (propietario_id),
    CONSTRAINTS propietario_rfc_uk UNIQUE (rfc),
    CONSTRAINTS propietario_curp_uk UNIQUE(curp)
);



-- 2 tablas relacionadas con constraints --
-- 1. Estudiante -  comprobante
CREATE TABLE estudiante(
    estudiante_id NUMERIC(10,0) NOT NULL,
    ap_paterno varchar(30) NOT NULL,
    ap_materno varchar(30) NOT NULL,
    CONSTRAINT estudiante_id_pk PRIMARY KEY (estudiante_id)
);
CREATE TABLE comprobante(
    comprobante_id numeric(10,0) NOT NULL,
    fecha_creado date not null,
    semestre varchar(6) not null,
    estudiante_id numeric(10,0) not null,
    CONSTRAINT comprobante_id_pk PRIMARY KEY (comprobante_id),
    CONSTRAINT estudante_id_fk FOREIGN KEY (estudiante_id) REFERENCES estudiante(estudiante_id) 
);