# NEXUS Tecnología

Tienda y servicio técnico de computadores: catálogo, carrito con pagos (efectivo y transferencia en sitio; transferencia y tarjeta con Wompi en línea), envíos nacionales, citas, "Arma tu PC", contacto y panel de administración.

Stack: TanStack Start (React 19) · Supabase · Wompi · Tailwind 4 · Nitro.

## Despliegue en Vercel

1. Sube este proyecto a GitHub (el repositorio `nexus`).
2. En Vercel: **Add New → Project** e importa el repositorio. Vercel detecta todo solo (usa `bun.lock`).
3. En **Settings → Environment Variables** agrega las variables de `.env.example`:

| Variable | Para qué sirve |
| --- | --- |
| `VITE_SUPABASE_URL`, `VITE_SUPABASE_PUBLISHABLE_KEY`, `VITE_SUPABASE_PROJECT_ID` | Navegador (se incrustan al compilar) |
| `SUPABASE_URL`, `SUPABASE_PUBLISHABLE_KEY`, `SUPABASE_PROJECT_ID` | Servidor / SSR |
| `SUPABASE_SERVICE_ROLE_KEY` | Servidor: crea pedidos y valida precios. **Secreta** |
| `WOMPI_PUBLIC_KEY`, `WOMPI_INTEGRITY_SECRET`, `WOMPI_EVENTS_SECRET` | Pagos con Wompi. Secretas |

4. Pulsa **Deploy**. Si cambias una variable `VITE_*`, haz **Redeploy** (se leen al compilar).
5. En el panel de Wompi, configura la URL de eventos (webhook):
   `https://TU-DOMINIO.vercel.app/api/public/wompi/webhook`

El proyecto fija `nitro: { preset: "vercel" }` en `vite.config.ts`, así `vite build` genera `.vercel/output`. Dentro de Lovable ese ajuste se ignora, por lo que ambos entornos siguen funcionando.

## Desarrollo local

```sh
cp .env.example .env   # y completa los valores
bun install            # o: npm i --legacy-peer-deps
bun run dev
```

## Lovable

Este proyecto sigue conectado con [Lovable](https://lovable.dev/projects/90e9b02d-164d-478f-a7dc-84037b244c8f). Los cambios que se suban a `main` en GitHub se sincronizan con el editor.
