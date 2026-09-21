# CampusLands CLI (Node.js)

Gestor de campers en **Node.js puro** con **EcmaScript Modules (ESM)**, sin dependencias externas. Permite registrar, listar y buscar campers, almacenando la información en un archivo JSON.

## Características

- **Node.js puro**: sin dependencias externas ni frameworks.
- **ESM (EcmaScript Modules)**: usa `import` / `export` (`"type": "module"`).
- **Persistencia en JSON**: los datos se guardan en `data/campers.json`.
- **CLI por argumentos**: comandos rápidos desde la terminal.
- **Modo interactivo**: registro guiado con preguntas en consola.

## Estructura del proyecto

```
campuslands-cli-node/
├── data/
│   └── campers.json        # Base de datos JSON de campers
├── src/
│   ├── campers.js          # Lógica de negocio (CRUD sobre JSON)
│   ├── index.js            # Punto de entrada CLI (argumentos)
│   └── interactivo.js      # Modo interactivo (readline)
├── package.json
└── README.md
```

## Uso

### 1. Listar campers

```bash
node src/index.js listar
```

Muestra todos los campers registrados en formato de tabla. Si no hay campers, muestra un mensaje informativo.

### 2. Agregar un camper

```bash
node src/index.js agregar "Carlos Morales" "Node.js"
```

Registra un nuevo camper con:

- `id`: autoincremental.
- `nombre`: nombre del camper.
- `stack`: stack tecnológico.
- `creadoEn`: fecha de creación.

> Si no se ingresan `nombre` y `stack`, se muestra un error.

### 3. Buscar un camper por nombre

```bash
node src/index.js buscar "Carlos"
```

Busca campers cuyo nombre contenga el término indicado.

### 4. Modo interactivo

```bash
node src/interactivo.js
```

Registro guiado paso a paso:

```
=== REGISTRO INTERACTIVO DE CAMPERS (ESM) ===
¿Nombre del camper? Ana López
¿Stack tecnológico? Node.js
🎉 Registrado en JSON: { id: 2, nombre: 'Ana López', stack: 'Node.js', creadoEn: '21/9/2026' }
```

## Cómo funciona

### `src/campers.js`

Contiene la lógica de negocio:

| Función                  | Descripción                                        |
| ------------------------ | -------------------------------------------------- |
| `leerCampers()`          | Lee y parsea `data/campers.json`. Si no existe, devuelve `[]`. |
| `guardarCampers(lista)`  | Escribe la lista de campers en el JSON.            |
| `agregarCamper(nombre, stack)` | Valida los datos, crea el camper con `id` autoincremental y lo guarda. |
| `listarCampers()`        | Devuelve todos los campers.                        |
| `buscarCamperPorNombre(termino)` | Filtra campers cuyo nombre contenga el término (case-insensitive). |

### `src/index.js`

Punto de entrada del CLI. Lee los argumentos de `process.argv` y ejecuta el comando correspondiente:

```
node src/index.js [listar | agregar | buscar]
```

### `src/interactivo.js`

Usa `node:readline/promises` para hacer preguntas al usuario y registrar un camper de forma interactiva.

## Formato de datos

Cada camper se almacena así en `data/campers.json`:

```json
[
  {
    "id": 1,
    "nombre": "Carlos Morales",
    "stack": "Node.js",
    "creadoEn": "21/9/2026"
  }
]
```

## Tecnologías

- **Node.js** — Entorno de ejecución.
- **ESM (EcmaScript Modules)** — Sistema de módulos nativo.
- **`node:fs/promises`** — Lectura/escritura asíncrona de archivos.
- **`node:readline/promises`** — Entrada interactiva por consola.
- **JSON** — Persistencia de datos.
