# Generador de alumnos

Herramienta web para generar registros de alumnos ficticios en SQL, CSV y JSON.

> Proyecto universitario — Base de Datos 2
> Universidad de Sonora · Marzo 2026

---

## 👤 Autor

Damian de Jesus Enriquez Solorzano · [@damianenriquez680](https://github.com/damianenriquez680)

## 🙏 Agradecimientos

Gracias al profesor **Jose Humberto Abril Garcia** por su apoyo y orientación durante el desarrollo de este proyecto.

---

## Instalación rápida

No requiere instalación ni servidor. Solo necesitas un navegador y conexión a internet (Tailwind se carga por CDN).

```bash
git clone https://github.com/damianenriquez680/<nombre-del-repositorio>.git
cd <nombre-del-repositorio>
# Abrir generador.html en el navegador
```

---

## Estructura

```
generador-alumnos/
├── generador.html      # Interfaz (frontend)
└── functions.js        # Lógica de generación y descarga
```

---

## Tecnologías

- **HTML5** y **JavaScript** puro (sin frameworks)
- **Tailwind CSS** vía CDN para los estilos

---

## Cómo se usa

1. Elige el **número de registros** (de 1 a 50,000; hay botones rápidos para Min y Max).
2. Selecciona el **formato de salida**.
3. Pulsa **⚡ Generar Registros** para ver la vista previa.
4. Pulsa **💾 Descargar Archivo** para guardar el resultado (`alumnos.sql`, `alumnos.csv` o `alumnos.json`).

---

## Formatos de salida

| Opción | Formato | Archivo |
|--------|---------|---------|
| SQL MySQL / MariaDB | `CREATE DATABASE` + `CREATE TABLE` + `INSERT` | `alumnos.sql` |
| PostgreSQL | En desarrollo (por ahora genera el mismo script que MySQL) | `alumnos.sql` |
| CSV (Excel) | Valores separados por comas con encabezado | `alumnos.csv` |
| JSON | Arreglo de objetos | `alumnos.json` |

---

## Entidades

### Tabla `alumnos` (base de datos `sistema_escolar`)
| Campo      | Tipo         | Descripción                              |
|------------|--------------|------------------------------------------|
| expediente | INT          | Matrícula única, inicia en 224250000     |
| app1       | VARCHAR(255) | Primer apellido (mexicano, en mayúsculas)|
| app2       | VARCHAR(255) | Segundo apellido (ruso), admite `NULL`   |
| nombres    | VARCHAR(255) | Un nombre, o nombre mexicano + francés   |
| correo     | VARCHAR(255) | Correo único `a<expediente>@unison.mx`   |

Restricciones: `UNIQUE` en `expediente` y en `correo`. Motor `InnoDB` con charset `utf8mb4`.

---

## Datos generados

- **Primer apellido:** elegido al azar de una lista de 100 apellidos mexicanos.
- **Segundo apellido:** elegido al azar de una lista de apellidos rusos; puede salir `NULL` para probar campos opcionales.
- **Nombres:** un nombre mexicano, y con 50% de probabilidad se le agrega un nombre francés como segundo nombre.
- **Matrícula y correo:** consecutivos a partir de `224250000`, con correo institucional `a<matrícula>@unison.mx`.

---

## Ejemplo de salida (SQL)

```sql
CREATE DATABASE IF NOT EXISTS sistema_escolar;
USE sistema_escolar;

CREATE TABLE IF NOT EXISTS alumnos (
  expediente int NOT NULL,
  app1 varchar(255) NOT NULL,
  app2 varchar(255) DEFAULT NULL,
  nombres varchar(255) NOT NULL,
  correo varchar(255) NOT NULL,
  UNIQUE KEY expediente (expediente),
  UNIQUE KEY correo (correo)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

INSERT INTO alumnos (expediente, app1, app2, nombres, correo) VALUES
(224250000, 'HERNÁNDEZ', 'PETROV', 'Juan Sophie', 'a224250000@unison.mx'),
(224250001, 'GARCÍA', NULL, 'Luis', 'a224250001@unison.mx');
```

---

## Para qué sirve

- Poblar bases de datos de práctica con miles de registros.
- Probar consultas, índices y restricciones (`UNIQUE`, `NULL`).
- Generar datos de prueba sin usar información real de personas.

---

## 🎓 Contexto académico

Proyecto académico para la materia de Base de Datos 2 — Universidad de Sonora, 2026.
Todos los datos generados son ficticios.