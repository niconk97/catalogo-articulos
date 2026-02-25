# Catálogo de Artículos - Aplicación de Escritorio

## Enunciado

Se necesita una aplicación para la gestión de artículos de un catálogo de un comercio. La aplicación debe ser genérica, es decir, aplicar para cualquier tipo de comercio; y la información que en ella se cargue será consumida luego desde distintos servicios para ser mostradas ya sea en webs, e-commerces, apps mobile, revistas, etc. Esto no es parte del desarrollo, pero sí del contexto en el cual se utilizará la aplicación a desarrollar.

## Descripción

Deberá ser una aplicación de escritorio que contemple la administración de artículos.

### Funcionalidades requeridas:

- Listado de artículos
- Búsqueda de artículos por distintos criterios
- Agregar artículos
- Modificar artículos
- Eliminar artículos
- Ver detalle de un artículo

Toda ésta información deberá ser persistida en una base de datos ya existente (la cual se adjunta).

### Datos del Artículo

Los datos mínimos con los que deberá contar el artículo son los siguientes:

- **Código de artículo**
- **Nombre**
- **Descripción**
- **Marca** (seleccionable de una lista desplegable)
- **Categoría** (seleccionable de una lista desplegable)
- **Imagen**
- **Precio**

## Etapas de Desarrollo

### Etapa 1
Construir las clases necesarias para el modelo de dicha aplicación junto a las ventanas con las que contará y su navegación.

### Etapa 2
Construir la interacción con la base de datos y validaciones correspondiente para dar vida a la funcionalidad.

## Consideraciones

La aplicación debe manejar:
- ? Arquitectura en capas
- ? Manejo de excepciones
- ? Validaciones cuando corresponda

## Modo de Entrega

- ? No deben realizar modificaciones en la DB, ante cualquier duda, me consultan.
- ?? Deben entregar un zip con la solución dentro con el nombre **TPFinalNivel2_Apellido**, por ejemplo: `TPFinalNivel2_SarFernandez`
- ??? Pueden eliminar las carpetas "bin" para achicar el tamaño del archivo final, esto es opcional.

---

## Script de Generación de Base de Datos

```sql
USE master
GO

CREATE DATABASE CATALOGO_DB
GO

USE CATALOGO_DB
GO

-- Configuración
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO

-- Tabla MARCAS
CREATE TABLE [dbo].[MARCAS](
    [Id] [int] IDENTITY(1,1) NOT NULL,
    [Descripcion] [varchar](50) NULL,
    CONSTRAINT [PK_MARCAS] PRIMARY KEY CLUSTERED 
    (
        [Id] ASC
    ) WITH (
        PAD_INDEX = OFF, 
        STATISTICS_NORECOMPUTE = OFF, 
        IGNORE_DUP_KEY = OFF, 
        ALLOW_ROW_LOCKS = ON, 
        ALLOW_PAGE_LOCKS = ON
    ) ON [PRIMARY]
) ON [PRIMARY]
GO

SET ANSI_PADDING OFF
GO

-- Tabla CATEGORIAS
CREATE TABLE [dbo].[CATEGORIAS](
    [Id] [int] IDENTITY(1,1) NOT NULL,
    [Descripcion] [varchar](50) NULL,
    CONSTRAINT [PK_CATEGORIAS] PRIMARY KEY CLUSTERED 
    (
        [Id] ASC
    ) WITH (
        PAD_INDEX = OFF, 
        STATISTICS_NORECOMPUTE = OFF, 
        IGNORE_DUP_KEY = OFF, 
        ALLOW_ROW_LOCKS = ON, 
        ALLOW_PAGE_LOCKS = ON
    ) ON [PRIMARY]
) ON [PRIMARY]
GO

SET ANSI_PADDING OFF
GO

-- Tabla ARTICULOS
CREATE TABLE [dbo].[ARTICULOS](
    [Id] [int] IDENTITY(1,1) NOT NULL,
    [Codigo] [varchar](50) NULL,
    [Nombre] [varchar](50) NULL,
    [Descripcion] [varchar](150) NULL,
    [IdMarca] [int] NULL,
    [IdCategoria] [int] NULL,
    [ImagenUrl] [varchar](1000) NULL,
    [Precio] [money] NULL,
    CONSTRAINT [PK_ARTICULOS] PRIMARY KEY CLUSTERED 
    (
        [Id] ASC
    ) WITH (
        PAD_INDEX = OFF, 
        STATISTICS_NORECOMPUTE = OFF, 
        IGNORE_DUP_KEY = OFF, 
        ALLOW_ROW_LOCKS = ON, 
        ALLOW_PAGE_LOCKS = ON
    ) ON [PRIMARY]
) ON [PRIMARY]
GO

SET ANSI_PADDING OFF
GO

-- Datos iniciales: MARCAS
INSERT INTO MARCAS VALUES 
    ('Samsung'), 
    ('Apple'), 
    ('Sony'), 
    ('Huawei'), 
    ('Motorola')
GO

-- Datos iniciales: CATEGORIAS
INSERT INTO CATEGORIAS VALUES 
    ('Celulares'),
    ('Televisores'), 
    ('Media'), 
    ('Audio')
GO

-- Datos iniciales: ARTICULOS
INSERT INTO ARTICULOS VALUES 
    ('S01', 'Galaxy S10', 'Una canoa cara', 1, 1, 
     'https://images.samsung.com/is/image/samsung/assets/ar/p6_gro2/p6_initial_mktpd/smartphones/galaxy-s10/specs/galaxy-s10-plus_specs_design_colors_prism_black.jpg?$163_346_PNG$', 
     69.999),
    ('M03', 'Moto G Play 7ma Gen', 'Ya siete de estos?', 5, 1, 
     'https://www.motorola.cl/arquivos/moto-g7-play-img-product.png?v=636862863804700000', 
     15699),
    ('S99', 'Play 4', 'Ya no se cuantas versiones hay', 3, 3, 
     'sin_imagen_para_que_de_error....muejeje', 
     35000),
    ('S56', 'Bravia 55', 'Alta tele', 3, 2, 
     'https://intercompras.com/product_thumb_keepratio_2.php?img=images/product/SONY_KDL-55W950A.jpg&w=650&h=450', 
     49500),
    ('A23', 'Apple TV', 'lindo loro', 2, 3, 
     'https://store.storeimages.cdn-apple.com/4668/as-images.apple.com/is/rfb-apple-tv-4k?wid=1144&hei=1144&fmt=jpeg&qlt=80&.v=1513897159574', 
     7850)
GO
```

## Estructura de la Base de Datos

### Tabla: MARCAS
| Campo | Tipo | Descripción |
|-------|------|-------------|
| Id | int (Identity) | Clave primaria |
| Descripcion | varchar(50) | Nombre de la marca |

### Tabla: CATEGORIAS
| Campo | Tipo | Descripción |
|-------|------|-------------|
| Id | int (Identity) | Clave primaria |
| Descripcion | varchar(50) | Nombre de la categoría |

### Tabla: ARTICULOS
| Campo | Tipo | Descripción |
|-------|------|-------------|
| Id | int (Identity) | Clave primaria |
| Codigo | varchar(50) | Código del artículo |
| Nombre | varchar(50) | Nombre del artículo |
| Descripcion | varchar(150) | Descripción del artículo |
| IdMarca | int | Clave foránea a MARCAS |
| IdCategoria | int | Clave foránea a CATEGORIAS |
| ImagenUrl | varchar(1000) | URL de la imagen |
| Precio | money | Precio del artículo |