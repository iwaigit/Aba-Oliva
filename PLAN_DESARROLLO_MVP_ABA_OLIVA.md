# Plan de Desarrollo MVP - Aba & Oliva 🇻🇪

**Versión:** 2.0 (MVP Visual + Backend Escalable)  
**Última actualización:** 04.02.2026  
**Estado:** En Desarrollo  
**Equipo:** 1 Developer (Full-stack)  
**Timeline:** 8 semanas (extensible)  

---

## 📋 Resumen Ejecutivo

App web en **Vercel** con **catálogo visual atractivo** sincronizado con **Printful API**. Backend escalable con **Convex** para manejo de órdenes. **Prioridad:** UI/UX limpia y funcional (catálogo → detalle → carrito → checkout).

**Stack:** Next.js 14 + TypeScript + TailwindCSS + Convex

---

## 🎯 MVP Core (Semanas 1-4)

### ✅ Must-Have
- Catálogo visual con precios e imágenes
- Página detalle producto con mockup
- Carrito funcional (Convex realtime)
- Checkout → Crear orden Printful
- Deploy Vercel

### ⏭️ Post-MVP (Semanas 5-8)
- Autenticación usuario
- Historial órdenes
- Webhooks Printful
- Notificaciones email
- Panel admin básico

---

## 🏗️ Arquitectura (Escalable desde día 1)

```
┌─────────────────────────────────────────┐
│     VERCEL (Frontend + API Routes)      │
│  Next.js 14 | React | TailwindCSS       │
└────────────────────┬────────────────────┘
                     │ API Endpoints
        ┌────────────┼────────────┐
        │            │            │
   ┌────▼─────┐  ┌──▼────┐  ┌───▼──────┐
   │  Printful │  │ Convex│  │ Email    │
   │    API    │  │  DB   │  │ Service  │
   └──────────┘  └───────┘  └──────────┘
```

---

## 📦 Stack Tecnológico

| Componente | Tecnología | Versión | Razón |
|-----------|-----------|---------|-------|
| **Framework** | Next.js | 14.x | SSR + API routes integradas |
| **Lenguaje** | TypeScript | 5.x | Type-safety end-to-end |
| **Estilos** | TailwindCSS | 3.x | Rápido, componentes listos |
| **BD Realtime** | Convex | Latest | Sin servidor, actualización automática |
| **Deploy** | Vercel | v1 | Mismo creador de Next.js |
| **API Client** | Fetch / SWR | Built-in | Lightweight, caché automático |

---

## 🗂️ Estructura de Carpetas

```
aba-oliva-app/
├── .env.local                # Variables locales (NO a git)
├── .env.example              # Plantilla variables
├── .gitignore               
│
├── src/
│   ├── app/
│   │   ├── layout.tsx        # Layout global con header/footer
│   │   ├── page.tsx          # Home (hero + catálogo)
│   │   │
│   │   ├── catalog/
│   │   │   └── page.tsx      # Catálogo completo con filtros
│   │   │
│   │   ├── products/
│   │   │   └── [id]/
│   │   │       └── page.tsx  # Detalle producto + carrito
│   │   │
│   │   ├── cart/
│   │   │   └── page.tsx      # Resumen carrito
│   │   │
│   │   ├── checkout/
│   │   │   └── page.tsx      # Formulario + crear orden
│   │   │
│   │   ├── api/
│   │   │   ├── printful/
│   │   │   │   ├── products/route.ts        # GET productos
│   │   │   │   ├── mockup/route.ts          # POST mockup preview
│   │   │   │   └── orders/route.ts          # POST crear orden
│   │   │   │
│   │   │   └── webhooks/
│   │   │       └── printful/route.ts        # Eventos Printful
│   │   │
│   │   └── success/
│   │       └── page.tsx      # Confirmación orden
│   │
│   ├── components/
│   │   ├── Header.tsx        # Nav + logo
│   │   ├── Footer.tsx        # Footer
│   │   ├── ProductCard.tsx   # Card individual
│   │   ├── ProductGrid.tsx   # Grid de cards
│   │   ├── ProductDetail.tsx # Detalle con mockup
│   │   ├── Cart/
│   │   │   ├── CartSidebar.tsx
│   │   │   └── CartItem.tsx
│   │   └── Checkout/
│   │       ├── CheckoutForm.tsx
│   │       └── PaymentInfo.tsx
│   │
│   ├── lib/
│   │   ├── printful.ts       # Cliente Printful (wrapper escalable)
│   │   ├── convex.ts         # Setup cliente Convex
│   │   ├── api-client.ts     # HTTP client genérico
│   │   └── utils.ts          # Helpers (formatPrice, etc)
│   │
│   ├── hooks/
│   │   ├── usePrintful.ts    # Query productos/mockup
│   │   ├── useCart.ts        # useQuery/useMutation carrito
│   │   └── useProducts.ts    # Queries productos
│   │
│   ├── types/
│   │   ├── printful.ts       # Tipos Printful API
│   │   ├── cart.ts           # Tipos carrito
│   │   ├── order.ts          # Tipos orden
│   │   └── product.ts        # Tipos producto
│   │
│   └── context/
│       └── CartContext.tsx   # Context para carrito global
│
├── convex/
│   ├── schema.ts             # Definición tablas (orders, carts)
│   ├── orders.ts             # Mutations/queries órdenes
│   ├── carts.ts              # Mutations/queries carrito
│   └── http.ts               # Funciones HTTP (webhooks)
│
├── public/
│   ├── designs/              # Imágenes de diseños (MACUNDALES, NOARRIMA)
│   ├── logo.svg
│   └── favicon.ico
│
├── docs/
│   ├── API.md                # Documentación endpoints
│   ├── CONVEX_SETUP.md       # Setup Convex
│   └── DEPLOYMENT.md         # Deploy Vercel
│
├── package.json
├── tsconfig.json
├── tailwind.config.ts
├── next.config.js
└── README.md
```

---

## 📅 Plan Semanal (8 semanas)

### **SEMANA 1: Setup + Estructura Base**

**Objetivo:** Proyecto corriendo en local + estructura lista

#### Tasks:
- [ ] Crear repo GitHub `aba-oliva-app`
- [ ] `npx create-next-app@latest aba-oliva --typescript --tailwind --app`
- [ ] Instalar deps: `npm install convex axios swr zustand`
- [ ] Setup Convex: `npx convex dev`
- [ ] Crear estructura carpetas (src/app, src/components, etc)
- [ ] Setup TypeScript + tsconfig.json
- [ ] Crear Header.tsx + Footer.tsx básicos
- [ ] Obtener API Key Printful
- [ ] Crear `.env.example`

**Entreg ables:**
- ✅ Proyecto corriendo en `localhost:3000`
- ✅ Estructura lista para code
- ✅ Git con primeros commits

**Horas:** 12-16h

---

### **SEMANA 2: Integración Printful + Backend API**

**Objetivo:** Backend completamente funcional para productos

#### Tasks:

**2.1 - Cliente Printful Wrapper** (`src/lib/printful.ts`)
```typescript
// Métodos principales:
export async function fetchProducts() { }          // GET /v2/products
export async function getProduct(id: number) { }   // GET /v2/products/{id}
export async function generateMockup(design) { }   // POST /v2/mockups
export async function createOrder(order) { }       // POST /v2/orders
export async function getOrderStatus(id) { }       // GET /v2/orders/{id}
```

**2.2 - API Routes Endpoints**
- [ ] `GET /api/printful/products` → List productos con cache
- [ ] `GET /api/printful/products/[id]` → Detalle producto
- [ ] `POST /api/printful/mockup` → Genera preview
- [ ] `POST /api/printful/orders` → Crea orden (sin auth aún)

**2.3 - Tipos TypeScript** (`src/types/`)
- [ ] `printful.ts` - Tipos Printful API
- [ ] `product.ts` - Tipos producto interno
- [ ] `order.ts` - Tipos orden

**2.4 - Convex Schema** (`convex/schema.ts`)
```typescript
export default defineSchema({
  orders: defineTable({
    printfulOrderId: v.string(),
    customerEmail: v.string(),
    customerName: v.string(),
    items: v.array(v.object({ /* ... */ })),
    status: v.enum('pending', 'confirmed', 'shipped'),
    total: v.number(),
    createdAt: v.number()
  }).index('by_email', ['customerEmail']),
  
  carts: defineTable({
    sessionId: v.string(),  // Temporal, sin auth aún
    items: v.array(v.object({ /* ... */ })),
    updatedAt: v.number()
  }).index('by_session', ['sessionId'])
});
```

**Entregas:**
- ✅ Endpoints funcionando
- ✅ Productos cargando desde Printful
- ✅ Tipos TS definidos

**Horas:** 16-20h

---

### **SEMANA 3: Frontend Catálogo (Visual Priority)**

**Objetivo:** Catálogo bonito, funcional y responsive

#### Tasks:

**3.1 - Home + Catálogo**
- [ ] Página home con hero section (Aba & Oliva brand)
- [ ] Catálogo grid responsive (3 cols desktop, 2 mobile, 1 tablet)
- [ ] ProductCard.tsx con:
  - Imagen producto
  - Título + descripción corta
  - Precio
  - Botón "Ver detalle"
  - Hover effect smooth
- [ ] Filtros básicos (categoría, precio)
- [ ] Search bar simple

**3.2 - Página Detalle Producto**
- [ ] Layout: imagen grande + info
- [ ] Mockup preview (Printful generate)
- [ ] Selector de talla/color (si aplica)
- [ ] Precio + disponibilidad
- [ ] Botón "Agregar al carrito"
- [ ] Descripción + definición del dicho (usando design back)

**3.3 - Diseño Visual**
- [ ] Color scheme: Negro primario (como franelas), blanco texto
- [ ] Tipografía: Clean (Inter/Poppins)
- [ ] Espaciado consistente (TailwindCSS utilities)
- [ ] Animaciones suaves (framer-motion opcional)
- [ ] Dark/Light mode considerar para futuro

**3.4 - SWR + Caché**
- [ ] Hook `usePrintful()` con SWR para productos
- [ ] Cache de imágenes/datos

**Entregas:**
- ✅ Home visualmente atractivo
- ✅ Catálogo completo con 5-10 diseños
- ✅ Detalle producto funcional
- ✅ Responsive mobile/tablet/desktop
- ✅ Carga rápida (<2s)

**Horas:** 20-24h

---

### **SEMANA 4: Carrito + Checkout (MVP Core)**

**Objetivo:** Flujo completo compra (sin autenticación aún)

#### Tasks:

**4.1 - Carrito Funcional**
- [ ] CartContext con Convex mutation
- [ ] Guardar carrito en Convex (sessionId temporal)
- [ ] CartSidebar.tsx (ver items, eliminar, cantidad)
- [ ] Página `/cart` con resumen
- [ ] Total price calculation
- [ ] Sincronización realtime (Convex)

**4.2 - Checkout**
- [ ] Página `/checkout`
- [ ] Formulario customer:
  - Nombre
  - Email
  - Teléfono
  - Dirección completa
- [ ] Resumen orden
- [ ] Botón "Crear Orden"

**4.3 - Crear Orden Printful**
- [ ] API Route `POST /api/printful/orders` que:
  1. Valida datos checkout
  2. Crea orden en Printful
  3. Guarda en Convex
  4. Retorna confirmación
- [ ] Página success `/success?orderId=xxx`
- [ ] Email confirmación básico (opcional semana 4)

**4.4 - Deploy Vercel**
- [ ] Setup dominio custom
- [ ] Environment vars en Vercel
- [ ] Deploy rama `main`
- [ ] Test en producción

**Entregas:**
- ✅ MVP completamente funcional
- ✅ Puedes vender franelas
- ✅ Deploy en Vercel con dominio custom
- ✅ Órdenes en Printful + Convex

**Horas:** 16-20h

**🎉 FIN MVP (4 semanas)** 

---

## 📅 Plan Post-MVP (Semanas 5-8)

### **SEMANA 5: Autenticación + Historial**

**Objetivo:** Usuarios pueden trackear sus órdenes

#### Tasks:
- [ ] NextAuth.js setup (email/password o Google)
- [ ] Tabla `users` en Convex
- [ ] Proteger rutas (`/admin`, `/orders`)
- [ ] Página `/orders` - historial órdenes user
- [ ] Vincular órdenes a user en Convex

**Horas:** 12-16h

---

### **SEMANA 6: Webhooks + Notificaciones**

**Objetivo:** Actualizar estado órdenes automáticamente

#### Tasks:
- [ ] Registrar webhook en Printful dashboard
- [ ] `POST /api/webhooks/printful` que:
  - Valida firma
  - Actualiza status en Convex
  - Envía email al customer
- [ ] Integrar SendGrid / Resend para email

**Horas:** 10-12h

---

### **SEMANA 7: Admin Panel Básico**

**Objetivo:** Dashboard simple para gestionar órdenes

#### Tasks:
- [ ] Página `/admin` (solo admin)
- [ ] Tabla órdenes (filtrable por status)
- [ ] KPIs: total ventas, órdenes hoy, trending products
- [ ] Exportar CSV órdenes

**Horas:** 12-16h

---

### **SEMANA 8: Pulido + Buffer**

**Objetivo:** Optimizar, ajustar bugs, documentación

#### Tasks:
- [ ] Lighthouse score > 90
- [ ] SEO: meta tags, OpenGraph
- [ ] Analytics (Vercel Analytics)
- [ ] Documentación README + DEPLOYMENT.md
- [ ] Testing manual end-to-end
- [ ] Buffer para fixes

**Horas:** 16-20h

---

## 💾 Convex Schema (Core)

```typescript
// convex/schema.ts
import { defineSchema, defineTable } from 'convex/server';
import { v } from 'convex/values';

export default defineSchema({
  // Órdenes con Printful
  orders: defineTable({
    printfulOrderId: v.string(),
    userId: v.optional(v.id('users')),        // Post-MVP
    customerEmail: v.string(),
    customerName: v.string(),
    customerPhone: v.string(),
    customerAddress: v.string(),
    items: v.array(v.object({
      productId: v.number(),
      variantId: v.number(),
      quantity: v.number(),
      price: v.number(),
      title: v.string()
    })),
    total: v.number(),
    paymentMethod: v.optional(v.string()),    // Futuro
    status: v.enum('pending', 'confirmed', 'shipped', 'delivered'),
    createdAt: v.number(),
    updatedAt: v.number()
  })
  .index('by_email', ['customerEmail'])
  .index('by_status', ['status'])
  .index('by_userId', ['userId']),

  // Carrito temporal
  carts: defineTable({
    sessionId: v.string(),                    // Cambiar a userId post-MVP
    items: v.array(v.object({
      productId: v.number(),
      variantId: v.number(),
      quantity: v.number(),
      price: v.number(),
      title: v.string()
    })),
    updatedAt: v.number()
  })
  .index('by_session', ['sessionId']),

  // Post-MVP
  users: defineTable({
    email: v.string(),
    name: v.string(),
    createdAt: v.number()
  })
  .index('by_email', ['email'])
});
```

---

## 📊 Tipos TypeScript (Core)

```typescript
// src/types/product.ts
export interface Product {
  id: number;
  title: string;
  description: string;
  brand: string;
  model: string;
  image: string;
  price: number;
  variants: Variant[];
}

export interface Variant {
  id: number;
  title: string;      // Ej: "Black - M"
  color: string;
  size: string;
  sku: string;
  retail_price: number;
}

// src/types/order.ts
export interface Order {
  id: string;
  printfulOrderId: string;
  customerEmail: string;
  customerName: string;
  items: OrderItem[];
  total: number;
  status: 'pending' | 'confirmed' | 'shipped' | 'delivered';
  createdAt: Date;
}

export interface OrderItem {
  productId: number;
  variantId: number;
  quantity: number;
  price: number;
  title: string;
}

// src/types/cart.ts
export interface CartItem {
  productId: number;
  variantId: number;
  quantity: number;
  price: number;
  title: string;
}
```

---

## 🔗 Integración Printful - Endpoints Críticos

| Endpoint | Método | Propósito |
|----------|--------|----------|
| `/v2/products` | GET | Catálogo completo |
| `/v2/products/{id}` | GET | Detalle producto |
| `/v2/mockups` | POST | Generar preview diseño |
| `/v2/orders` | POST | Crear orden |
| `/v2/orders/{id}` | GET | Estado orden |
| `/v2/webhooks` | POST | Registrar webhook |

### Estructura Orden Printful (Crear)
```json
{
  "recipient": {
    "name": "Juan Pérez",
    "address1": "Calle Principal 123",
    "city": "Caracas",
    "state_code": "DC",
    "country_code": "VE",
    "zip": "1010"
  },
  "items": [
    {
      "product_id": 1,
      "variant_id": 123,
      "quantity": 1
    }
  ],
  "shipping": "STANDARD"
}
```

---

## 🔐 Variables de Entorno

```bash
# .env.local (NUNCA a git)
NEXT_PUBLIC_PRINTFUL_API_KEY=xxxxxxxxxxxxx
NEXT_PUBLIC_CONVEX_URL=https://xxxxx.convex.cloud
NEXT_PUBLIC_API_URL=http://localhost:3000

# Printful webhook secret
WEBHOOK_SECRET=xxxxxxxxxxxxx

# Post-MVP
NEXTAUTH_SECRET=xxxxxxxxxxxxx
NEXTAUTH_URL=https://aba-oliva.vercel.app
SMTP_HOST=smtp.gmail.com
SMTP_USER=xxx@gmail.com
SMTP_PASS=xxxxxxxxxxxxx
```

---

## 🚀 Setup Inicial (Primeros 30 minutos)

```bash
# 1. Crear proyecto
npx create-next-app@latest aba-oliva --typescript --tailwind --app

# 2. Instalar dependencias
cd aba-oliva
npm install convex axios swr zustand

# 3. Inicializar Convex
npx convex dev

# 4. Setup Vercel git
git init
git remote add origin https://github.com/tuusername/aba-oliva-app.git

# 5. Crear .env.local con API keys
echo "NEXT_PUBLIC_PRINTFUL_API_KEY=xxxx" > .env.local
echo ".env.local" >> .gitignore
```

---

## 📈 Hitos Visibles

| Semana | Hito | URL | Status |
|--------|------|-----|--------|
| 1 | Setup completo | localhost:3000 | ✅ |
| 2 | Productos cargando | /catalog | ✅ |
| 3 | Catálogo visual | / | ✅ |
| 4 | MVP en vivo | vercel.app | ✅ |
| 5 | Login + historial | /orders | ⏭️ |
| 6 | Webhooks activos | Printful events | ⏭️ |
| 7 | Admin dashboard | /admin | ⏭️ |
| 8 | Producción lista | GO-LIVE | ⏭️ |

---

## 💡 Consejos Ejecución (1 dev)

1. **Commits pequeños** - Push daily al repo
2. **Convex local primero** - `npx convex dev` antes de deploy
3. **Printful sandbox** - Usa API key de test antes de live
4. **TailwindCSS presets** - Crea componentes reutilizables
5. **Skipea perfección** - MVP debe ser "good enough", no "perfect"
6. **Backup semanal** - Export órdenes Convex/Printful

---

## 📚 Documentación Clave

- [Convex Docs](https://docs.convex.dev)
- [Next.js 14](https://nextjs.org/docs)
- [Printful API](https://developers.printful.com/docs)
- [TailwindCSS](https://tailwindcss.com/docs)

---

## ✍️ Notas Finales

- **Extensión posible:** Si necesitas más tiempo, el plan es modular (puedes pausar en semana 4)
- **Scope creep:** Evita agregar features, sigue el plan
- **Feedback temprano:** Lanza MVP en semana 4, itera con usuarios reales
- **Scalability:** Backend diseñado para crecer (Convex + Printful + Vercel serverless)

---

**Desarrollado para:** Aba & Oliva 🇻🇪  
**Versión:** 2.0 MVP-focused  
**Última actualización:** 04.02.2026
