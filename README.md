# Proyecto Full Stack - Gestión de Usuarios y Blog

Este proyecto es una aplicación Full Stack que utiliza **Laravel** para el backend con autenticación proporcionada por **Laravel Breeze**, y **Angular** para el frontend. El backend maneja un sistema de gestión de usuarios, autenticación, y un CRUD de posts con categorías. El frontend consume la API del backend y permite la interacción del usuario con los datos.

## Requisitos

- **PHP >= 8.0**
- **Composer**
- **Node.js >= 16.x** y **npm**
- **PostgreSQL**
- **Docker** (opcional, para simplificar el entorno de desarrollo)
- **Angular CLI** (si vas a trabajar en el frontend)
  
## Estructura del Proyecto

- `backend/`: Aplicación Laravel.
- `frontend/`: Aplicación Angular.
- `docker-compose.yml`: Definición de servicios para backend, frontend, PostgreSQL, y Redis (opcional).

---

## Instalación

### Backend (Laravel)

1. Clona el repositorio y navega a la carpeta `backend`:
   ```bash
   git clone https://github.com/usuario/proyecto.git
   cd proyecto/backend
   ```

2. Instala las dependencias de PHP:
   ```bash
   composer install
   ```

3. Copia el archivo `.env.example` a `.env`:
   ```bash
   cp .env.example .env
   ```

4. Configura las variables de entorno en el archivo `.env`:
   ```env
   DB_CONNECTION=pgsql
   DB_HOST=127.0.0.1
   DB_PORT=5432
   DB_DATABASE=nombre_de_la_base_de_datos
   DB_USERNAME=nombre_de_usuario
   DB_PASSWORD=contraseña
   ```

5. Genera la clave de la aplicación de Laravel:
   ```bash
   php artisan key:generate
   ```

6. Crea la base de datos en PostgreSQL y ejecuta las migraciones:
   ```bash
   php artisan migrate
   ```

7. Opcional: Si estás utilizando **Docker**, ejecuta los servicios:
   ```bash
   docker-compose up --build
   ```

8. Inicia el servidor de Laravel:
   ```bash
   php artisan serve
   ```

### Frontend (Angular)

1. Navega a la carpeta `frontend`:
   ```bash
   cd ../frontend
   ```

2. Instala las dependencias de Node.js:
   ```bash
   npm install
   ```

3. Inicia el servidor de Angular:
   ```bash
   ng serve
   ```

El frontend estará disponible en `http://localhost:4200`.

---

## Docker

Si prefieres usar **Docker** para simplificar la configuración del entorno de desarrollo, asegúrate de tener **Docker** instalado y ejecuta el siguiente comando en la raíz del proyecto:

```bash
docker-compose up --build
```

Esto levantará los servicios para:

- **Angular** (frontend) en `http://localhost:4200`
- **Laravel** (backend) en `http://localhost:8000`
- **PostgreSQL** como base de datos
- **Redis** como caché (opcional)

---

## Endpoints del Backend (API)

### Autenticación de Usuarios

- **POST** `/api/register`: Registro de nuevos usuarios.
- **POST** `/api/login`: Inicio de sesión de usuarios.
- **POST** `/api/logout`: Cierre de sesión (requiere autenticación).
- **GET** `/api/profile`: Obtener perfil del usuario autenticado (requiere autenticación).

### Gestión de Posts

- **GET** `/api/posts/{categoryid}`: Listar todos los posts de una categoría.
- **POST** `/api/posts`: Crear un nuevo post (requiere autenticación).
- **PUT** `/api/posts/{id}`: Actualizar un post (requiere autenticación).
- **DELETE** `/api/posts/{id}`: Eliminar un post (requiere autenticación).

### Gestión de Categorías

- **GET** `/api/categories/{parentcategoryid}`: Listar las categorías contenidas en una categoría superior.
- **POST** `/api/categories`: Crear una nueva categoría (requiere autenticación).

---

## Pruebas Unitarias

El proyecto incluye pruebas unitarias para las siguientes funcionalidades clave:

1. Registro de usuarios.
2. Inicio de sesión de usuarios.

Para ejecutar las pruebas, usa el siguiente comando:

```bash
php artisan test
```

---

## Notas de Desarrollo

- **Autenticación**: Se utiliza **Laravel Breeze** para implementar la autenticación con sesión, y se asegura que solo los usuarios autenticados puedan acceder a las rutas protegidas.
- **Seguridad**: Las contraseñas se almacenan de manera segura utilizando el hash de bcrypt y se utilizan políticas de acceso para que solo los creadores de posts puedan actualizarlos o eliminarlos.
- **Validación**: Se implementa validación tanto del lado del cliente (en Angular) como del servidor (en Laravel) para los formularios de registro y login.