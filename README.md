# Exactum – Frontend

Interfaz web de **Exactum**, aplicación para organizar las finanzas de personas naturales (espacio *Personal*) y de emprendedores (espacio *Emprendimiento*). Proyecto Pedagógico Integrador (PPI) del Tecnológico de Antioquia, Equipo 02.

**Aplicación en línea:** https://fronted-exactum.vercel.app

## Tecnologías

- React con Vite
- React Router (`react-router-dom`)
- HTML, CSS y JavaScript
- Docker (nginx) como opción de despliegue
- Despliegue en Vercel

## Funcionalidades

- **Acceso:** registro, inicio de sesión y recuperación de contraseña.
- **Personal:** dashboard, movimientos, categorías, presupuestos, reportes y perfil.
- **Emprendimiento:** registro de *Mi negocio* (obligatorio antes de ver el resto), dashboard, inventario, clientes, proveedores, ventas, gastos, cuentas por cobrar y por pagar, y reportes.

## Estructura

```
src/
├── pages/         Pantallas (Login, Dashboard, Movements, Emprendimiento...)
├── components/    Componentes reutilizables (por ejemplo NegocioGate)
├── routes/        Rutas de la aplicación
└── services/      Llamadas al backend (API_URL)
public/
vercel.json        Redirección de rutas hacia index.html
Dockerfile         Build con Node y servidor nginx
```

## Variables de entorno

La URL del backend se lee con `import.meta.env.VITE_API_URL`, por lo que no se escribe fija en el código.

`.env` (desarrollo):

```dotenv
VITE_API_URL=http://localhost:3000
```

`.env.production` (producción), sin `/` al final:

```dotenv
VITE_API_URL=https://backend-exactum.onrender.com
```

En Vercel se configura esta misma variable en *Environment Variables*.

## Ejecución local

Requiere Node.js 22 o superior y el backend corriendo.

```bash
npm install
npm run dev
```

Para generar la versión de producción:

```bash
npm run build
```

Los archivos quedan en la carpeta `dist`.

## Despliegue en Vercel

1. Importar el repositorio desde GitHub.
2. Si el proyecto está dentro de una subcarpeta, indicarla en *Root Directory*.
3. Configurar:
   - **Framework Preset:** Vite
   - **Build Command:** `npm run build`
   - **Output Directory:** `dist`
   - **Variable:** `VITE_API_URL` con la URL del backend
4. Pulsar *Deploy*.

El archivo `vercel.json` redirige todas las rutas a `index.html`, para que recargar páginas como `/dashboard` no dé error 404.

## Ejecución con Docker (opcional)

```bash
docker build -t exactum-frontend .
docker run -p 8080:80 exactum-frontend
```

## Nota

El backend está en el plan gratuito de Render: si lleva un rato sin uso, la primera petición (por ejemplo el login) puede tardar 50 segundos o más.

## Equipo

Santiago Henao, Manuel Henao, Leandro Hurtado y Andrés Camilo Alzate – Tecnológico de Antioquia.
