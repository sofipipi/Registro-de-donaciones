# Registro-de-donaciones

# Base del Proyecto

Proyecto web basado en una arquitectura separada entre frontend, backend y base de datos. Todos los servicios se ejecutan mediante **Docker Compose**.

## Stack tecnológico

### Frontend

- **React** — biblioteca para la construcción de la interfaz de usuario.
- **Vite** — herramienta de desarrollo y build.
- **TypeScript** — tipado estático.
- **Tailwind CSS** — framework de estilos.

### Backend

- **NestJS** — framework para la construcción de la API.
- **TypeScript** — lenguaje principal.
- **Axios** — cliente HTTP para realizar solicitudes a servicios externos.
- **Prisma** — ORM utilizado para interactuar con la base de datos.

### Base de datos

- **PostgreSQL** — sistema gestor de base de datos relacional.

### Infraestructura

- **Docker** — contenedorización de los servicios.
- **Docker Compose** — orquestación de los contenedores.

---

## Arquitectura

La aplicación está dividida en tres servicios principales:

```text
                    Docker Compose
┌──────────────────────────────────────────────┐
│                                              │
│  ┌─────────────┐       ┌─────────────┐      │
│  │  Frontend   │       │   Backend   │      │
│  │             │ Axios │             │      │
│  │ React       │──────→│ NestJS      │      │
│  │ Vite        │       │ TypeScript  │      │
│  │ TypeScript  │       │ Axios       │      │
│  │ Tailwind    │       │ Prisma      │      │
│  │             │       │             │      │
│  │   :5173     │       │   :3000     │      │
│  └─────────────┘       └──────┬──────┘      │
│                               │             │
│                            Prisma            │
│                               │             │
│                               ↓             │
│                       ┌─────────────┐       │
│                       │  PostgreSQL  │       │
│                       │             │       │
│                       │   :5432     │       │
│                       └─────────────┘       │
│                                              │
└──────────────────────────────────────────────┘


### Flujo 

React
  ↓
Axios
  ↓
NestJS
  ↓
Prisma ORM
  ↓
PostgreSQL


Levantar el proyecto

desde la raiz:
docker compose up --build -d

Detener el proyecto

docker compose down -v

Puertos

Frontend → http://localhost:5173
Backend  → http://localhost:3000
Database → localhost:5432

Migraciones de Prisma

crear una migracion

docker compose exec backend npx prisma migrate dev --name nombre_migracion

Generar cliente de prisma

docker compose exec backend npx prisma generate

Abrir prisma

docker compose exec backend npx prisma studio

