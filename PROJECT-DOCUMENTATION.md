# FríaCheck - Guía Rápida

Sistema web para gestionar equipos de refrigeración.

---

## ¿Qué es?

Aplicación para que técnicos y administradores gestionen:
- **Máquinas** de refrigeración
- **Visitas** técnicas en terreno
- **Tickets** de soporte
- **Pedidos** y ventas
- **Reportes**

---

## ¿Qué necesitas?

- Node.js 18+
- Angular CLI 17+
- npm o yarn

---

## Instalación

```bash
npm install
npm start
```

Abre http://localhost:4200

---

## Usuarios y Roles

| Rol | ¿Qué puede hacer? |
|-----|-------------------|
| **super-admin** | Ver todas las empresas, métricas globales |
| **support** | Ver empresas, editar usuarios |
| **admin** | Gestionar su empresa, máquinas, usuarios |

---

## Páginas principales

| Ruta | Descripción |
|------|-------------|
| `/login` | Iniciar sesión |
| `/dashboard` | Panel principal (métricas, gráficos) |
| `/activos` | Lista de máquinas |
| `/visitas` | Registro de visitas técnicas |
| `/tickets` | Tickets de soporte |
| `/pedidos` | Gestión de pedidos |
| `/locales` | Mapa de locales |
| `/reportes` | Generación de reportes |
| `/usuarios` | CRUD de usuarios |
| `/perfil` | Tu perfil |
| `/tenants` | Empresas (solo super-admin) |

---

## Estructura del proyecto

```
src/app/
├── core/           # Servicios base (auth, guards)
├── features/       # Páginas y funcionalidades
│   ├── auth/       # Login
│   ├── dashboard/  # Panel principal
│   ├── machines/   # Máquinas/Activos
│   ├── visits/    # Visitas
│   ├── tickets/   # Tickets
│   └── ...
└── shared/         # Componentes reutilizables
```

---

## Configuración

Edita `src/environments/environment.ts`:

```typescript
export const environment = {
  production: false,
  apiUrl: 'https://friocheckweb.azurewebsites.net/api/v1',
  googleMapsApiKey: 'TU_KEY',
};
```

---

## Comandos útiles

| Comando | Acción |
|---------|--------|
| `npm start` | Iniciar servidor (desarrollo) |
| `npm run build` | Compilar para producción |
| `npm test` | Ejecutar tests |

---

## Autenticación

1. El usuario ingresa email + password
2. El backend devuelve un JWT (token)
3. El token se guarda en sessionStorage
4. Cada request incluye el token en el header `Authorization`
5. Dependiendo del rol, se redirige al dashboard correspondiente

---

## NFC y GPS

- Las visitas técnicas se validan con **tags NFC** y **ubicación GPS**
- El técnico hace check-in/check-out desde el móvil

---

## Tema claro/oscuro

Cambia automáticamente o manualmente desde la barra superior.

---

**Versión:** 1.0.0 | **Fecha:** Abril 2026