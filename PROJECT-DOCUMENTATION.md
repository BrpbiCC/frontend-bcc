# FríaCheck - Documentación Técnica del Frontend

> Documentación completa del proyecto de frontend Angular para el sistema de gestión FríaCheck.
> **Versión:** 1.0.0 | **Última actualización:** Abril 2026

---

## Tabla de Contenidos

1. [Resumen del Proyecto](#1-resumen-del-proyecto)
2. [Tecnologías y Dependencias](#2-tecnologías-y-dependencias)
3. [Estructura del Proyecto](#3-estructura-del-proyecto)
4. [Arquitectura de la Aplicación](#4-arquitectura-de-la-aplicación)
5. [Módulos y Funcionalidades](#5-módulos-y-funcionalidades)
6. [Sistema de Autenticación y RBAC](#6-sistema-de-autenticación-y-rbac)
7. [Servicios Core](#7-servicios-core)
8. [Componentes de Layout](#8-componentes-de-layout)
9. [Rutas y Navegación](#9-rutas-y-navegación)
10. [Variables de Entorno](#10-variables-de-entorno)
11. [Guía de Instalación](#11-guía-de-instalación)
12. [Comandos Disponibles](#12-comandos-disponibles)

---

## 1. Resumen del Proyecto

### Descripción General

**FríaCheck** es una aplicación web frontend desarrollada en Angular para la gestión de equipos de refrigeración. El sistema permite:

- **Autenticación multi-tenant** con JWT y control de acceso basado en roles (RBAC)
- **Dashboard interactivo** con métricas globales y de empresa en tiempo real
- **Gestión de activos** (máquinas de refrigeración) vinculados con tags NFC
- **Registro de visitas** de técnicos en terreno con validación GPS
- **Sistema de tickets** de soporte y seguimiento
- **Gestión de ventas** y pedidos
- **Reportes y métricas** exportables
- **Tema claro/oscuro** con persistencia

### Características Principales

| Característica | Descripción |
|----------------|-------------|
| Multi-tenant | Cada empresa (tenant) tiene acceso isolated a sus datos |
| RBAC | Control de acceso granular por roles (SUPER_ADMIN, SUPPORT, ADMIN) |
| Tiempo real | Dashboard con métricas actualizadas en tiempo real |
| NFC/GPS | Validación de visitas con tags NFC y ubicación GPS |
| Responsive | Diseño adaptativo para escritorio y dispositivos móviles |
| Tema | Soporte para modo claro y oscuro |

---

## 2. Tecnologías y Dependencias

### Framework y Lenguaje

| Tecnología | Versión | Propósito |
|------------|---------|-----------|
| Angular | 21.2+ | Framework principal |
| TypeScript | 5.9+ | Lenguaje de programación |
| Node.js | 18+ | Entorno de ejecución |

### Dependencias de Producción

| Paquete | Versión | Propósito |
|---------|---------|-----------|
| `@angular/core` | 21.2.0 | Core de Angular |
| `@angular/material` | 21.2.4 | Componentes UI (Material Design) |
| `@angular/cdk` | 21.2.4 | Toolkit de componentes |
| `@angular/router` | 21.2.0 | Sistema de rutas |
| `@angular/forms` | 21.2.0 | Formularios reactivos |
| `@angular/google-maps` | 21.2.6 | Mapa de locales |
| `chart.js` | 4.5.1 | Gráficos y visualización |
| `rxjs` | 7.8.0 | Programación reactiva |
| `zone.js` | 0.15.1 | Zona de cambio de Angular |

### Dependencias de Desarrollo

| Paquete | Versión | Propósito |
|---------|---------|-----------|
| `@angular/cli` | 21.2.3 | CLI de Angular |
| `@angular/compiler-cli` | 21.2.0 | Compilación TypeScript |
| `typescript` | 5.9.2 | Compilador de TypeScript |
| `vitest` | 4.0.8 | Tests unitarios |
| `prettier` | 3.8.1 | Formateo de código |
| `jsdom` | 28.0.0 | DOM virtual para tests |

---

## 3. Estructura del Proyecto

### Árbol de Directorios

```
frontend/
├── angular.json              # Configuración de Angular CLI
├── package.json              # Dependencias y scripts
├── tsconfig.json             # Configuración TypeScript
├── README.md                  # Documentación general
├── RBAC-README.md             # Documentación del sistema RBAC
├── arquitectura/              # Documentación de arquitectura backend
│   └── ARQUITECTURA.md
├── documentation/             # Documentación adicional
├── public/                   # Recursos estáticos públicos
│   └── imagenes/
│       └── logos/            # Logos de la aplicación
├── src/
│   ├── index.html            # HTML principal
│   ├── main.ts               # Punto de entrada
│   ├── styles.css            # Estilos globales
│   ├── material-theme.scss   # Tema de Angular Material
│   ├── app/
│   │   ├── app.ts            # Componente raíz
│   │   ├── app.component.ts  # Componente principal
│   │   ├── app.routes.ts     # Definición de rutas
│   │   ├── app.config.ts     # Configuración de la app
│   │   ├── app.component.html
│   │   ├── app.component.css
│   │   │
│   │   ├── core/             # Servicios y lógica core
│   │   │   ├── components/
│   │   │   │   └── layout/
│   │   │   │       ├── sidebar/       # Barra lateral de navegación
│   │   │   │       ├── topbar/        # Barra superior
│   │   │   │       ├── topbar-mobile/ # Barra superior móvil
│   │   │   │       └── theme-switcher/ # Cambio de tema
│   │   │   │
│   │   │   ├── services/
│   │   │   │   ├── auth/             # Servicio de autenticación
│   │   │   │   ├── locales.service.ts
│   │   │   │   ├── view-history.service.ts
│   │   │   │   └── nfc-tags.service.ts
│   │   │   │
│   │   │   ├── guards/
│   │   │   │   ├── auth.guard.ts     # Protección de rutas autenticadas
│   │   │   │   └── role.guard.ts     # Protección por roles
│   │   │   │
│   │   │   ├── interceptors/
│   │   │   │   └── auth.interceptor.ts # Intercepta requests HTTP
│   │   │   │
│   │   │   ├── models/
│   │   │   │   └── local.model.ts
│   │   │   │
│   │   │   └── config/
│   │   │       ├── filter.service.ts
│   │   │       └── chile-locations.service.ts
│   │   │
│   │   ├── features/         # Módulos de funcionalidad
│   │   │   ├── auth/
│   │   │   │   ├── login/
│   │   │   │   │   ├── login.ts
│   │   │   │   │   └── login.html
│   │   │   │   └── pages/
│   │   │   │       └── unauthorized/
│   │   │   │
│   │   │   ├── dashboard/
│   │   │   │   ├── pages/dashboard/
│   │   │   │   └── services/
│   │   │   │       └── dashboard-realtime.service.ts
│   │   │   │
│   │   │   ├── machines/
│   │   │   │   ├── pages/activos/
│   │   │   │   ├── services/
│   │   │   │   └── models/
│   │   │   │
│   │   │   ├── visits/
│   │   │   │   ├── pages/visitas/
│   │   │   │   └── services/
│   │   │   │
│   │   │   ├── tickets/
│   │   │   │   ├── pages/tickets/
│   │   │   │   ├── pages/ticket-detail/
│   │   │   │   └── services/
│   │   │   │
│   │   │   ├── sales/
│   │   │   │   ├── pages/pedidos/
│   │   │   │   └── services/
│   │   │   │
│   │   │   ├── locales/
│   │   │   │   └── pages/locales/
│   │   │   │
│   │   │   ├── reportes/
│   │   │   │   └── pages/reportes/
│   │   │   │
│   │   │   ├── usuarios/
│   │   │   │   └── pages/usuarios/
│   │   │   │
│   │   │   ├── perfil/
│   │   │   │   └── pages/perfil/
│   │   │   │
│   │   │   ├── tenants/
│   │   │   │   ├── pages/tenants/
│   │   │   │   └── pages/tenant-detail/
│   │   │   │
│   │   │   ├── metricas-globales/
│   │   │   │   └── pages/metricas-globales/
│   │   │   │
│   │   │   └── role-selector/
│   │   │       └── role-selector.ts
│   │   │
│   │   ├── shared/           # Componentes y servicios compartidos
│   │   │   ├── components/
│   │   │   │   ├── logo/              # Componente logo dinámico
│   │   │   │   ├── map/               # Mapa de locales
│   │   │   │   ├── filters/           # Filtros de búsqueda
│   │   │   │   └── view-search-filters/
│   │   │   │
│   │   │   ├── dialogs/
│   │   │   │   ├── confirm-dialog.component.ts
│   │   │   │   ├── confirm-dialog.component.html
│   │   │   │   └── confirm-dialog.service.ts
│   │   │   │
│   │   │   ├── directives/
│   │   │   │   └── click-outside.directive.ts
│   │   │   │
│   │   │   └── material/
│   │   │       └── material.module.ts
│   │   │
│   │   └── styles/
│   │       ├── colors.css
│   │       └── app.css
│   │
│   ├── environments/
│   │   └── environment.ts
│   │
│   └── assets/
│       └── images/
│           └── logo/
│               ├── logo-light.svg
│               └── logo-dark.svg
```

### Descripción de Carpetas Principales

| Carpeta | Descripción |
|---------|-------------|
| `core/` | Servicios fundamentales (auth, guards, interceptors) |
| `features/` | Módulos de negocio organizados por funcionalidad |
| `shared/` | Componentes, directivas y servicios reutilizables |
| `environments/` | Configuraciones por entorno (dev/prod) |
| `assets/` | Recursos estáticos (imágenes, fuentes) |

---

## 4. Arquitectura de la Aplicación

### Patrón de Diseño

La aplicación sigue un patrón de **componentes standalone** de Angular, con:

```
┌─────────────────────────────────────────────────────────┐
│                    AppComponent                          │
│  (Raíz - maneja sidebar, topbar, tema)                   │
└─────────────────────────────────────────────────────────┘
                           │
            ┌──────────────┼──────────────┐
            ▼              ▼              ▼
    ┌────────────┐ ┌────────────┐ ┌────────────┐
    │   Sidebar  │ │   Topbar   │ │ RouterOutlet│
    │ (Navegación)│ │  (Header) │ │  (Contenido)│
    └────────────┘ └────────────┘ └────────────┘
                                      │
                    ┌─────────────────┼─────────────────┐
                    ▼                 ▼                 ▼
            ┌────────────┐   ┌─��──────────┐   ┌────────────┐
            │  Dashboard │   │   Activos  │   │   Visitas  │
            │   (Home)    │   │  (Máquinas)│   │  (Técnico) │
            └────────────┘   └────────────┘   └────────────┘
```

### Flujo de Datos

```
┌──────────┐     ┌───────────┐     ┌────────────┐
│  UI      │────▶│ Component │────▶│  Service   │
│(Template)│◀────│  (TS)     │◀────│  (Lógica)  │
└──────────┘     └───────────┘     └────────────┘
                                       │
                                       ▼
                                  ┌────────────┐
                                  │ HTTP Client│
                                  └────────────┘
                                       │
                                       ▼
                                  ┌────────────┐
                                  │   Backend  │
                                  │   (API)    │
                                  └────────────┘
```

### Modelo de Estado

La aplicación maneja estado de tres formas:

| Tipo | Descripción | Uso |
|------|-------------|-----|
| **Services con BehaviorSubject** | Estado reactivo en servicios inyectables | Auth, Filtros, Dashboard |
| **LocalStorage/sessionStorage** | Persistencia de datos del usuario | Token, tema, preferencias |
| **@Input/@Output** | Estado entre componentes padre/hijo | Datos de formularios, eventos |

---

## 5. Módulos y Funcionalidades

### 5.1 Módulo de Autenticación

**Ubicación:** `src/app/features/auth/`

| Componente | Descripción |
|------------|-------------|
| `login/` | Página de inicio de sesión con email/password |
| `unauthorized/` | Página para usuarios sin permisos |

**Características:**
- Login con email y contraseña
- Extracción de roles desde JWT
- Redirección según rol después del login
- Persistencia de sesión en sessionStorage

### 5.2 Módulo de Dashboard

**Ubicación:** `src/app/features/dashboard/`

| Ruta | Descripción | Roles permitidos |
|------|-------------|------------------|
| `/dashboard` | Dashboard principal | Todos |
| `/dashboard/admin` | Dashboard admin | admin |
| `/dashboard/support` | Dashboard soporte | support, admin |
| `/dashboard/superadmin` | Dashboard superadmin | super-admin |

**Características:**
- Métricas en tiempo real
- Gráficos de rendimiento
- Estadísticas de visitas y máquinas
- Actualización automática cada 30 segundos

### 5.3 Módulo de Máquinas/Activos

**Ubicación:** `src/app/features/machines/`

| Componente | Descripción |
|------------|-------------|
| `activos/` | Lista y gestión de equipos de refrigeración |

**Modelo de datos:**
```typescript
interface Machine {
  id: string;
  name: string;
  type: string;
  brand: string;
  model: string;
  serialNumber: string;
  nfcTagId: string;
  status: 'OPERATIVE' | 'MAINTENANCE' | 'OUT_OF_SERVICE';
  latitude: number;
  longitude: number;
  clientName: string;
  clientAddress: string;
}
```

### 5.4 Módulo de Visitas

**Ubicación:** `src/app/features/visits/`

| Componente | Descripción |
|------------|-------------|
| `visitas/` | Registro de visitas de técnicos |

**Características:**
- Check-in con NFC + GPS
- Check-out con validación
- Notas y registro de temperatura
- Historial de visitas por técnico

### 5.5 Módulo de Tickets

**Ubicación:** `src/app/features/tickets/`

| Componente | Descripción |
|------------|-------------|
| `tickets/` | Lista de tickets de soporte |
| `ticket-detail/` | Detalle y edición de ticket |

**Estados:** `open` → `in_progress` → `resolved` → `closed`

**Prioridades:** `low`, `medium`, `high`, `urgent`

### 5.6 Módulo de Ventas/Pedidos

**Ubicación:** `src/app/features/sales/`

| Componente | Descripción |
|------------|-------------|
| `pedidos/` | Gestión de pedidos y ventas |

### 5.7 Módulo de Locales

**Ubicación:** `src/app/features/locales/`

| Componente | Descripción |
|------------|-------------|
| `locales/` | Mapa interactivo de locales |

**Características:**
- Mapa con Google Maps
- Filtros por sector y estado
- Información detallada al seleccionar

### 5.8 Módulo de Reportes

**Ubicación:** `src/app/features/reportes/`

| Componente | Descripción |
|------------|-------------|
| `reportes/` | Generación de reportes |

### 5.9 Módulo de Usuarios

**Ubicación:** `src/app/features/users/`

| Componente | Descripción |
|------------|-------------|
| `usuarios/` | CRUD de usuarios del tenant |

### 5.10 Módulo de Perfil

**Ubicación:** `src/app/features/perfil/`

| Componente | Descripción |
|------------|-------------|
| `perfil/` | Perfil del usuario actual |

### 5.11 Módulo de Tenants

**Ubicación:** `src/app/features/tenants/`

| Componente | Descripción |
|------------|-------------|
| `tenants/` | Lista de empresas (solo SUPER_ADMIN) |
| `tenant-detail/` | Detalle de empresa |

**Rutas protegidas:** Solo `super-admin`

### 5.12 Módulo de Métricas Globales

**Ubicación:** `src/app/features/metricas-globales/`

| Componente | Descripción |
|------------|-------------|
| `metricas-globales/` | Métricas cross-tenant |

**Rutas protegidas:** Solo `super-admin`

---

## 6. Sistema de Autenticación y RBAC

### 6.1 Roles del Sistema

| Rol | Descripción | Permisos principales |
|-----|-------------|---------------------|
| `super-admin` | Administrador global | Ver todos los tenants, métricas globales, crear tenants |
| `support` | Soporte técnico | Ver tenants, editar usuarios |
| `admin` | Administrador de empresa | Gestionar su tenant, usuarios, máquinas |

### 6.2 Servicio de Autenticación

**Archivo:** `src/app/core/services/auth/auth.service.ts`

```typescript
// Interfaz de sesión
interface AuthSession {
  token: string;
  role: 'admin' | 'support' | 'super-admin';
  tenantId: string | null;
  userName: string;
  userEmail: string;
  userId: string;
}
```

**Métodos principales:**

| Método | Descripción |
|--------|-------------|
| `login(credentials)` | Autentica usuario y persiste sesión |
| `logout()` | Limpia sesión y storage |
| `isAuthenticated()` | Verifica si hay sesión activa |
| `getToken()` | Obtiene JWT del storage |
| `getRole()` | Obtiene rol actual |
| `getTenantId()` | Obtiene ID del tenant |
| `getDashboardRoute(role)` | Devuelve ruta de dashboard según rol |

### 6.3 Guards de Protección

**AuthGuard (`src/app/core/guards/auth.guard.ts`):**
- Protege rutas que requieren autenticación
- Redirecciona a `/login` si no está autenticado
- Expone guards específicos: `dashboardRedirectGuard`, `publicOnlyGuard`

**RoleGuard (`src/app/core/guards/role.guard.ts`):**
- Protege rutas por rol específico
- Redirecciona a `/unauthorized` si el rol no coincide

### 6.4 Interceptor de Autenticación

**Archivo:** `src/app/core/interceptors/auth.interceptor.ts`

Agrega automáticamente el header `Authorization: Bearer <token>` a todas las requests HTTP.

### 6.5 Flujo de Login

```
1. Usuario ingresa email + password
         │
         ▼
2. AuthService.login() → POST /auth/login
         │
         ▼
3. Backend valida credenciales y devuelve JWT
         │
         ▼
4. AuthService persiste en sessionStorage:
   - token, role, tenantId, userName, userEmail, userId
         │
         ▼
5. AuthInterceptor agrega Bearer token a requests
         │
         ▼
6. Redirección según rol:
   - super-admin → /dashboard/superadmin
   - support → /dashboard/support
   - admin → /dashboard/admin
```

---

## 7. Servicios Core

### 7.1 AuthService

**Ubicación:** `src/app/core/services/auth/auth.service.ts`

Gestiona toda la autenticación y sesión del usuario.

### 7.2 FilterService

**Ubicación:** `src/app/core/config/filter.service.ts`

Gestiona filtros globales de la aplicación.

### 7.3 LocalesService

**Ubicación:** `src/app/core/services/locales.service.ts`

Obtiene y cachea información de locales.

### 7.4 DashboardRealtimeService

**Ubicación:** `src/app/features/dashboard/services/dashboard-realtime.service.ts`

Maneja métricas en tiempo real para el dashboard.

### 7.5 NFC Tags Service

**Ubicación:** `src/app/core/services/nfc-tags.service.ts`

Gestiona tags NFC para validación de visitas.

---

## 8. Componentes de Layout

### 8.1 Sidebar

**Ubicación:** `src/app/core/components/layout/sidebar/`

| Archivo | Descripción |
|---------|-------------|
| `sidebar.ts` | Componente TypeScript |
| `sidebar.html` | Template con navegación |

**Características:**
- Navegación colapsable
- Items de menú según rol
- Indicador de ruta activa
- Responsive (auto-colapsa en móvil)

### 8.2 Topbar

**Ubicación:** `src/app/core/components/layout/topbar/`

| Archivo | Descripción |
|---------|-------------|
| `topbar.ts` | Componente TypeScript |
| `topbar.html` | Template con user info |

**Características:**
- Logo de la aplicación
- Nombre del usuario
- Cambio de tema (light/dark)
- Menú de logout

### 8.3 Theme Switcher

**Ubicación:** `src/app/core/components/layout/theme-switcher/`

Permite cambiar entre tema claro y oscuro. Guarda preferencia en localStorage.

---

## 9. Rutas y Navegación

### 9.1 Definición de Rutas

**Archivo:** `src/app/app.routes.ts`

```typescript
export const routes: Routes = [
  // Rutas públicas
  { path: 'login', component: Login, canActivate: [publicOnlyGuard] },
  { path: 'unauthorized', component: Unauthorized },

  // Dashboard (con redirect según rol)
  { path: 'dashboard', component: Dashboard },
  { path: 'dashboard/admin', ... },
  { path: 'dashboard/support', ... },
  { path: 'dashboard/superadmin', ... },

  // Rutas protegidas por autenticación
  { path: 'activos', ... },
  { path: 'visitas', ... },
  { path: 'tickets', ... },
  { path: 'pedidos', ... },
  { path: 'locales', ... },
  { path: 'reportes', ... },
  { path: 'usuarios', ... },
  { path: 'perfil', ... },

  // Rutas protegidas por rol (super-admin)
  { path: 'tenants', ... },
  { path: 'metricas-globales', ... },

  // Redirects
  { path: '', redirectTo: '/login', pathMatch: 'full' },
  { path: '**', redirectTo: '/login' },
];
```

### 9.2 Matriz de Permisos por Ruta

| Ruta | Auth | admin | support | super-admin |
|------|------|-------|---------|-------------|
| `/login` | ❌ | - | - | - |
| `/dashboard` | ✅ | ✅ | ✅ | ✅ |
| `/dashboard/admin` | ✅ | ✅ | ❌ | ❌ |
| `/dashboard/support` | ✅ | ✅ | ✅ | ❌ |
| `/dashboard/superadmin` | ✅ | ❌ | ❌ | ✅ |
| `/activos` | ✅ | ✅ | ✅ | ✅ |
| `/visitas` | ✅ | ✅ | ✅ | ✅ |
| `/tickets` | ✅ | ✅ | ✅ | ✅ |
| `/pedidos` | ✅ | ✅ | ✅ | ✅ |
| `/locales` | ✅ | ✅ | ✅ | ✅ |
| `/reportes` | ✅ | ✅ | ✅ | ✅ |
| `/usuarios` | ✅ | ✅ | ✅ | ✅ |
| `/perfil` | ✅ | ✅ | ✅ | ✅ |
| `/tenants` | ✅ | ❌ | ❌ | ✅ |
| `/metricas-globales` | ✅ | ❌ | ❌ | ✅ |

---

## 10. Variables de Entorno

### Archivo: `src/environments/environment.ts`

```typescript
export const environment = {
  production: false,
  apiUrl: 'https://friocheckweb.azurewebsites.net/api/v1',
  googleMapsApiKey: 'AIzaSyD4MAk_pf9qCxAOX7rLBvpKVNHMG_aSHUo',
};
```

| Variable | Descripción |
|----------|-------------|
| `production` | Indica si es entorno de producción |
| `apiUrl` | URL base de la API del backend |
| `googleMapsApiKey` | API Key de Google Maps para el mapa de locales |

---

## 11. Guía de Instalación

### Prerrequisitos

- **Node.js** 18+ (recomendado: 20 LTS)
- **npm** 9+ o **yarn** 1.28+
- **Angular CLI** 17+ (opcional, para generar código)

### Pasos de Instalación

```bash
# 1. Navegar al directorio del proyecto
cd frontend

# 2. Instalar dependencias
npm install

# 3. Verificar versión instalada
npm list @angular/core
```

### Configuración

1. **Backend URL:** Editar `src/environments/environment.ts` para cambiar `apiUrl`
2. **Google Maps:** Editar `googleMapsApiKey` con tu API key válida

---

## 12. Comandos Disponibles

### Scripts de package.json

| Comando | Descripción |
|---------|-------------|
| `npm start` | Inicia servidor de desarrollo (http://localhost:4200) |
| `npm run build` | Construye aplicación para producción |
| `npm run build -- --configuration development` | Build de desarrollo con source maps |
| `npm test` | Ejecuta tests unitarios con Vitest |
| `npm run watch` | Watch mode para desarrollo |

### Comandos Angular CLI

```bash
# Generar nuevo componente
ng generate component features/nueva-funcionalidad

# Generar nuevo servicio
ng generate service core/services/mi-servicio

# Generar nuevo guard
ng generate guard core/guards/mi-guard

# Build de producción
ng build --configuration production
```

### Desarrollo Local

```bash
# Iniciar con hot-reload
npm start

# La app estará disponible en:
# http://localhost:4200
```

---

## Anexo: Modelos de Datos Principales

### UserContext (RBAC)

```typescript
interface UserContext {
  id: string;
  role: 'admin' | 'support' | 'super-admin';
  tenantId: string;
  username: string;
}
```

### Machine

```typescript
interface Machine {
  id: string;
  name: string;
  type: string;
  brand: string;
  model: string;
  serialNumber: string;
  nfcTagId: string;
  status: 'OPERATIVE' | 'MAINTENANCE' | 'OUT_OF_SERVICE' | 'PENDING_INSTALL' | 'INACTIVE';
  latitude: number;
  longitude: number;
  isActive: boolean;
  clientName: string;
  clientAddress: string;
}
```

### Visit

```typescript
interface Visit {
  id: string;
  tenantId: string;
  technicianId: string;
  machineId: string;
  latitude: number;
  longitude: number;
  nfcTagId: string;
  temperature?: number;
  notes?: string;
  status: 'pending' | 'completed' | 'flagged';
  type: 'MAINTENANCE' | 'SALE' | 'INSPECTION' | 'DELIVERY';
  visitedAt: Date;
}
```

---

## Anexo: API Endpoints Principales

### Autenticación

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| POST | `/auth/login` | Iniciar sesión |
| POST | `/auth/register` | Registrar usuario (admin) |
| POST | `/auth/forgot-password` | Solicitar recuperación |
| POST | `/auth/reset-password` | Restablecer contraseña |
| POST | `/auth/validate-token` | Validar JWT |

### Recursos

| Recurso | Endpoints principales |
|---------|----------------------|
| Users | GET/POST `/users`, GET/PUT/DELETE `/users/:id` |
| Machines | GET/POST `/machines`, GET `/machines/:id/nfc` |
| Visits | GET/POST `/visits`, POST `/visits/checkin`, POST `/visits/:id/checkout` |
| Tickets | GET/POST `/tickets`, GET/PUT `/tickets/:id` |
| Sales | GET/POST `/sales` |
| Tenants | GET/POST `/tenants` (super-admin) |

---

## Anexo: Temas y Estilos

### Variables CSS Principales

```css
:root {
  --primary-color: #1976d2;
  --accent-color: #ff4081;
  --background-light: #ffffff;
  --background-dark: #121212;
  --text-light: #000000;
  --text-dark: #ffffff;
}
```

### Tema Oscuro

El tema oscuro se activa con el atributo `data-theme="dark"` en `<html>`.

---

**Documentación generada:** Abril 2026
**Versión del frontend:** 1.0.0
**Framework:** Angular 21.2+