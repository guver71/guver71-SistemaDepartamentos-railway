# 🏠 Sistema de Departamentos

<div align="center">

![Laravel](https://img.shields.io/badge/Laravel-11-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)
![PHP](https://img.shields.io/badge/PHP-8.2-777BB4?style=for-the-badge&logo=php&logoColor=white)
![Livewire](https://img.shields.io/badge/Livewire-3-4EACA1?style=for-the-badge&logo=livewire&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-8-4479A1?style=for-the-badge&logo=mysql&logoColor=white)

![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![PHP Version](https://img.shields.io/badge/PHP-%3E%3D8.2-8892BF?style=for-the-badge)
![Laravel Version](https://img.shields.io/badge/Laravel-11-FF2D20?style=for-the-badge)

</div>

<p align="center">
  Sistema web completo para la <strong>gestión integral de alquileres de habitaciones y departamentos</strong>. 
  Control de propiedades, clientes, contratos, pagos, caja y generación de reportes.
</p>

---

## 📋 Tabla de Contenidos

- [Características](#-características)
- [Stack Tecnológico](#-stack-tecnológico)
- [Arquitectura del Sistema](#-arquitectura-del-sistema)
- [Requisitos Previos](#-requisitos-previos)
- [Instalación](#-instalación)
- [Configuración](#-configuración)
- [Base de Datos](#-base-de-datos)
- [Uso del Sistema](#-uso-del-sistema)
- [Estructura del Proyecto](#-estructura-del-proyecto)
- [Diagrama de Base de Datos](#-diagrama-de-base-de-datos)
- [Despliegue](#-despliegue)
- [Autor](#-autor)
- [Licencia](#-licencia)

---

## ✨ Características

### 🏢 Gestión de Propiedades
- CRUD completo de propiedades (inmuebles)
- Ubicación por ciudad y dirección
- Asociación de múltiples habitaciones por propiedad

### 🛏️ Gestión de Habitaciones
- Registro de habitaciones con precios individuales:
  - Precio de alquiler
  - Precio de luz
  - Precio de agua
- Tipos de habitación (simple, doble, suite, etc.)
- Indicador visual de disponibilidad (alquilada / libre)

### 👥 Gestión de Clientes
- Registro completo de datos personales
- Tipos y números de identificación
- Información de contacto (teléfono, email, dirección)
- Búsqueda por nombre, teléfono o dirección

### 📝 Sistema de Alquileres
- Asignación de clientes a habitaciones
- Control de estado (activo / liberado)
- Notas adicionales por contrato
- Liberación de habitaciones con un clic

### 💰 Sistema de Pagos
- Registro de pagos contra alquileres
- Cálculo automático del total (alquiler + luz + agua)
- Generación automática de **tickets en PDF**
- Apertura de ticket en nueva ventana

### 💵 Control de Caja
- Apertura de caja con monto inicial
- Seguimiento de ingresos y egresos en tiempo real
- Cálculo automático de saldo disponible
- Cierre de caja con fecha y monto gastado
- Solo una caja puede estar abierta simultáneamente

### 📊 Gestión de Gastos
- Registro de gastos con descripción y monto
- Carga de fotos/comprobantes (máx. 2MB)
- Filtrado por rango de fechas
- **Exportación a Excel** con filtros aplicados
- Validación de saldo disponible antes de registrar

### 📈 Dashboard
- Resumen de clientes, habitaciones y alquileres activos
- Gráfico de **alquileres por mes** (Chart.js)
- Gráfico de **pagos por mes** (Chart.js)
- Estadísticas actualizadas en tiempo real

### 🔐 Autenticación y Seguridad
- Sistema de login completo (Laravel Breeze)
- Rutas protegidas con middleware `auth`
- Gestión de perfil de usuario
- IDs encriptados en URLs sensibles

---

## 🛠️ Stack Tecnológico

| Capa | Tecnología | Versión |
|------|-----------|---------|
| **Backend** | Laravel | 11.x |
| **PHP** | PHP | >= 8.2 |
| **Frontend Interactivo** | Livewire | 3.x |
| **CSS Framework** | Tailwind CSS | 3.x |
| **Template Admin** | Stellar / Bootstrap Admin | - |
| **Gráficos** | Chart.js | 4.x |
| **Generación PDF** | DomPDF (barryvdh/laravel-dompdf) | 2.x |
| **Exportación Excel** | Maatwebsite Excel | 3.x |
| **Autenticación** | Laravel Breeze | 2.x |
| **Build Tool** | Vite | 5.x |
| **Base de Datos** | MySQL | 8.x |
| **Cache/Sessions** | Database (configurable) | - |
| **JavaScript** | Alpine.js + Axios | - |

---

## 🏗️ Arquitectura del Sistema

```
┌─────────────────────────────────────────────────────┐
│                    FRONTEND                          │
│  ┌─────────┐  ┌──────────┐  ┌──────────────────┐   │
│  │  Blade   │  │ Livewire │  │   Tailwind CSS   │   │
│  │ Templates│  │Components│  │  + Alpine.js     │   │
│  └─────────┘  └──────────┘  └──────────────────┘   │
├─────────────────────────────────────────────────────┤
│                    BACKEND                           │
│  ┌─────────┐  ┌──────────┐  ┌──────────────────┐   │
│  │ Routes  │  │Controllers│  │    Models        │   │
│  │  (web)  │  │  (Admin)  │  │  (Eloquent ORM)  │   │
│  └─────────┘  └──────────┘  └──────────────────┘   │
├─────────────────────────────────────────────────────┤
│                  SERVICIOS                           │
│  ┌──────────┐  ┌───────────┐  ┌─────────────────┐  │
│  │ DomPDF   │  │  Excel    │  │   Crypt/URLs    │  │
│  │ (Tickets)│  │ (Exports) │  │  (Seguridad)    │  │
│  └──────────┘  └───────────┘  └─────────────────┘  │
├─────────────────────────────────────────────────────┤
│               BASE DE DATOS                          │
│  ┌─────────────────────────────────────────────┐    │
│  │  MySQL 8  │  Cache  │  Sessions  │  Jobs    │    │
│  └─────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────┘
```

---

## 📦 Requisitos Previos

Antes de instalar el proyecto, asegúrate de tener:

- **PHP** >= 8.2 (con extensiones: mbstring, xml, curl, zip, gd, bcmath)
- **Composer** >= 2.x
- **Node.js** >= 18.x (con npm o yarn)
- **MySQL** >= 8.0
- **Git**

---

## 🚀 Instalación

### 1. Clonar el repositorio

```bash
git clone https://github.com/guver71/SistemaDepartamentos-railway.git
cd SistemaDepartamentos-railway
```

### 2. Instalar dependencias de PHP

```bash
composer install
```

### 3. Instalar dependencias de Node.js

```bash
npm install
```

### 4. Configurar el archivo `.env`

```bash
cp .env.example .env
```

Generar la clave de la aplicación:

```bash
php artisan key:generate
```

### 5. Configurar la base de datos

Edita el archivo `.env` con tus credenciales de MySQL:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=santatest
DB_USERNAME=root
DB_PASSWORD=tu_password
```

### 6. Ejecutar migraciones y seeders

```bash
php artisan migrate:fresh --seed
```

> **Nota:** Esto creará todas las tablas y el usuario administrador por defecto.

### 7. Compilar assets (opcional para desarrollo)

```bash
npm run dev
```

### 8. Iniciar el servidor

```bash
php artisan serve
```

El sistema estará disponible en: **http://localhost:8000**

---

## ⚙️ Configuración

### Credenciales por Defecto

| Campo | Valor |
|-------|-------|
| **Email** | `admin@gmail.com` |
| **Contraseña** | `admin123` |

> ⚠️ **IMPORTANTE:** Cambia estas credenciales después del primer login en producción.

### Variables de Entorno Importantes

```env
# Aplicación
APP_NAME="Sistema Departamentos"
APP_ENV=local          # Cambiar a 'production' en despliegue
APP_DEBUG=true         # false en producción
APP_URL=http://localhost:8000

# Base de Datos
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=santatest
DB_USERNAME=root
DB_PASSWORD=

# Sesiones y Cache (usar Redis o Memcached en producción)
SESSION_DRIVER=database
CACHE_STORE=database
QUEUE_CONNECTION=database
```

---

## 💾 Base de Datos

### Diagrama Entidad-Relación

```
┌──────────────┐       ┌──────────────┐
│  properties  │       │    types     │
│──────────────│       │──────────────│
│ id (PK)      │       │ id (PK)      │
│ name         │       │ name         │
│ city         │       │ description  │
│ address      │       └──────┬───────┘
└──────┬───────┘              │
       │ 1                    │ 1
       │                      │
       │ N                    │ N
┌──────┴───────┐              │
│    rooms     │◄─────────────┘
│──────────────│
│ id (PK)      │
│ rentalprice  │
│ lightprice   │
│ waterprice   │
│ number       │
│ property_id  │ (FK → properties)
│ type_id      │ (FK → types)
└──────┬───────┘
       │ 1
       │
       │ N
┌──────┴───────┐       ┌──────────────┐
│    rents     │       │   clients    │
│──────────────│       │──────────────│
│ id (PK)      │       │ id (PK)      │
│ note         │       │ full_name    │
│ status       │◄──────│ date_of_birth│
│ client_id    │ (FK)  │ gender       │
│ room_id      │ (FK)  │ phone        │
└──────┬───────┘       │ email        │
       │ 1             │ address      │
       │               │ city         │
       │ N             │ state        │
┌──────┴───────┐       │ postal_code  │
│   payments   │       │ country      │
│──────────────│       │ id_number    │
│ id (PK)      │       │ id_type      │
│ amount       │       └──────────────┘
│ rent_id      │ (FK → rents)
│ cashbox_id   │ (FK → cash_boxes)
└──────────────┘

┌──────────────┐       ┌──────────────┐
│  cash_boxes  │       │   expenses   │
│──────────────│       │──────────────│
│ id (PK)      │       │ id (PK)      │
│ initial_amt  │       │ description  │
│ spent        │       │ amount       │
│ closing_date │       │ photo        │
│ status       │       │ cashbox_id   │ (FK → cash_boxes)
│ user_id      │ (FK)  └──────────────┘
└──────────────┘
```

### Tablas del Sistema

| Tabla | Registros | Descripción |
|-------|-----------|-------------|
| `users` | N | Usuarios del sistema (autenticación) |
| `properties` | N | Propiedades/inmuebles |
| `types` | N | Tipos de habitación |
| `rooms` | N | Habitaciones disponibles |
| `clients` | N | Clientes registrados |
| `rents` | N | Contratos de alquiler |
| `payments` | N | Pagos realizados |
| `cash_boxes` | N | Aperturas/cierres de caja |
| `expenses` | N | Gastos registrados |

---

## 🖥️ Uso del Sistema

### Flujo de Trabajo

```
┌─────────────┐     ┌──────────────┐     ┌──────────────┐
│  1. Crear   │────▶│  2. Crear    │────▶│  3. Crear    │
│ Propiedades │     │  Habitaciones│     │  Clientes    │
└─────────────┘     └──────────────┘     └──────────────┘
                                               │
                                               ▼
┌─────────────┐     ┌──────────────┐     ┌──────────────┐
│  6. Cerrar  │◀────│  5. Registrar│◀────│  4. Alquilar │
│    Caja     │     │   Pagos      │     │ Habitación   │
└─────────────┘     └──────────────┘     └──────────────┘
       │
       ▼
┌─────────────┐
│  7. Ver     │
│ Dashboard   │
└─────────────┘
```

### Módulos Disponibles

| Ruta | Módulo | Descripción |
|------|--------|-------------|
| `/dashboard` | Tablero | Resumen y gráficos estadísticos |
| `/properties` | Propiedades | CRUD de inmuebles |
| `/types` | Tipos | Tipos de habitación |
| `/rooms` | Habitaciones | Gestión de habitaciones |
| `/clients` | Clientes | Gestión de clientes |
| `/rentals` | Alquileres | Lista de alquileres activos |
| `/cashboxs` | Caja | Control de apertura/cierre |
| `/expenses` | Gastos | Registro y exportación |
| `/users` | Usuarios | Gestión de usuarios |
| `/profile` | Perfil | Configuración de usuario |

### Generación de Tickets PDF

Al registrar un pago, se genera automáticamente un ticket PDF con:
- Datos de la propiedad y habitación
- Información del cliente
- Monto pagado
- Fecha y hora

El ticket se abre en una nueva ventana para impresión o descarga.

### Exportación de Gastos

Desde el módulo de gastos, puedes exportar a Excel (.xlsx) con:
- Filtro por rango de fechas
- Búsqueda por descripción o monto
- Columnas: Monto, Fecha/Hora, Descripción

---

## 📁 Estructura del Proyecto

```
SistemaDepartamentos-railway/
├── app/
│   ├── Exports/
│   │   └── ExpensesExport.php          # Exportación Excel de gastos
│   ├── Http/
│   │   └── Controllers/
│   │       ├── Admin/
│   │       │   └── RentController.php  # Controlador de alquileres
│   │       ├── Auth/                   # Autenticación (Breeze)
│   │       ├── Principal.php           # Dashboard y ruta principal
│   │       └── ProfileController.php   # Perfil de usuario
│   ├── Livewire/
│   │   └── Admin/
│   │       ├── CashComponent.php       # Componente de caja
│   │       ├── ClientComponent.php     # Componente de clientes
│   │       ├── ExpenseComponent.php    # Componente de gastos
│   │       ├── PaymentComponent.php    # Componente de pagos
│   │       ├── PropertyComponent.php   # Componente de propiedades
│   │       ├── RentalComponent.php     # Lista de alquileres
│   │       ├── RentComponent.php       # Crear alquiler
│   │       ├── RoomComponent.php       # Componente de habitaciones
│   │       ├── TypeComponent.php       # Tipos de habitación
│   │       └── UserComponent.php       # Gestión de usuarios
│   ├── Models/
│   │   ├── CashBox.php
│   │   ├── Client.php
│   │   ├── Expense.php
│   │   ├── Payment.php
│   │   ├── Property.php
│   │   ├── Rent.php
│   │   ├── Room.php
│   │   ├── Type.php
│   │   └── User.php
│   └── View/
├── database/
│   ├── migrations/                     # 11 migraciones
│   └── seeders/
│       ├── DatabaseSeeder.php
│       └── UserSeeder.php              # Usuario admin por defecto
├── public/
│   └── assets/admin/                   # Assets estáticos (CSS, JS, imágenes)
├── resources/
│   └── views/
│       ├── admin/
│       │   ├── dashboard.blade.php
│       │   ├── layouts/
│       │   │   ├── app.blade.php
│       │   │   └── partials/
│       │   └── rooms/
│       │       ├── payment.blade.php
│       │       ├── rent.blade.php
│       │       └── ticket.blade.php    # Template del ticket PDF
│       └── livewire/admin/             # 10 componentes Livewire
├── routes/
│   ├── auth.php
│   └── web.php                         # Rutas principales
├── .env                                # Configuración (no commitear)
├── composer.json
├── package.json
├── vite.config.js
└── tailwind.config.js
```

---

## 🌐 Despliegue en Railway

### Configuración para Railway

1. **Conectar el repositorio** a Railway
2. **Configurar variables de entorno** en el dashboard de Railway:

```env
APP_ENV=production
APP_DEBUG=false
APP_URL=https://tu-app.up.railway.app
DB_CONNECTION=mysql
DB_HOST=mysql.railway.internal
DB_PORT=3306
DB_DATABASE=railway
DB_USERNAME=root
DB_PASSWORD=tu_password_railway
```

3. **Agregar buildpack** o Dockerfile:

```dockerfile
FROM php:8.2-fpm

# Instalar extensiones
RUN apt-get update && apt-get install -y \
    git curl zip unzip libpng-dev libonig-dev \
    libxml2-dev libzip-dev zip

RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd zip

# Instalar Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

WORKDIR /var/www

COPY . .

RUN composer install --no-dev --optimize-autoloader
RUN php artisan config:cache
RUN php artisan route:cache
RUN php artisan view:cache

EXPOSE 8000

CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8000"]
```

4. **Ejecutar migraciones** después del despliegue:

```bash
railway run php artisan migrate --force
railway run php artisan db:seed --force
```

---

## 🔧 Comandos Útiles

```bash
# Desarrollo
php artisan serve              # Servidor local
npm run dev                    # Compilar assets en tiempo real
npm run build                  # Compilar para producción

# Base de datos
php artisan migrate            # Ejecutar migraciones pendientes
php artisan migrate:fresh      # Resetear y recrear BD
php artisan migrate:fresh --seed  # Resetear con datos de prueba
php artisan db:seed            # Ejecutar seeders

# Cache y optimización
php artisan config:cache       # Cachear configuración
php artisan route:cache        # Cachear rutas
php artisan view:cache         # Cachear vistas
php artisan optimize:clear     # Limpiar toda la caché

# Livewire
php artisan livewire:clear     # Limpiar componentes Livewire
```

---

## 🤝 Contribuir

Las contribuciones son bienvenidas. Para cambios grandes, por favor abre un issue primero.

1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/nueva-funcionalidad`)
3. Haz tus cambios
4. Confirma tus cambios (`git commit -m 'Add nueva funcionalidad'`)
5. Empuja a la rama (`git push origin feature/nueva-funcionalidad`)
6. Abre un Pull Request

---

## 📄 Licencia

Este proyecto está bajo la licencia MIT. Consulta el archivo [LICENSE](LICENSE) para más detalles.

---

## 👨‍💻 Autor

**Guver Ccori** - [GitHub](https://github.com/guver71)

---

<div align="center">

**¿Te resultó útil?** Dale una ⭐ al repositorio si te ayudó.

</div>
