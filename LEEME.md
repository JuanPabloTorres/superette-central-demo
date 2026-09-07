# Superette Central — Demo funcional

Demo de portal digital para negocios tipo superette/colmado (víveres, carnicería,
a granel), en el formato estándar de dos modos (Cliente / Negocio) que usa
Juan Pablo para presentar sistemas a clientes.

**Este es un demo genérico** — sin nombre de negocio real — pensado para
presentarlo a varios dueños de superette (ej. Superette Pastillo en Juana
Díaz, superettes de Villalba, etc.) y luego personalizarlo por cliente.

- **Repo:** https://github.com/JuanPabloTorres/superette-central-demo
- **Demo en vivo:** https://juanpablotorres.github.io/superette-central-demo/

## Cambios de esta revisión

- **Catálogo ampliado a 16 categorías** (antes 11): se separó "Higiene y Hogar" en
  **Limpieza del Hogar** y **Cuidado Personal**, y se agregaron **Ferretería y Hogar**,
  **Mascotas**, **Bebé** y **Farmacia y Salud** — las secciones que cualquier
  supermercado real tiene además de víveres. Catálogo pasó de ~55 a ~78 productos.
- **Descripción real en cada producto** (`descripcion` en `src/data/catalogo.js`),
  visible en la tarjeta del catálogo y en el detalle al agregar al carrito.
- **Más ofertas tipo shopper**: 4 promociones nuevas (Kit Básico del Hogar,
  Semana de Cuidado Personal, Combo Mascota Feliz, Bienvenida Bebé) además de
  las 4 originales — 8 en total, cubriendo todas las secciones nuevas.
- **Marca rediseñada**: el wordmark pasó de script cursivo a un logotipo sans-serif
  en mayúsculas con ícono de canasta — se ve a supermercado, no a pizzería/panadería.
- **Fondo y superficies**: se cambió la textura cálida de "papel de estraza" por un
  gris-verde frío y sutil, más de piso de tienda que de menú de restaurante.
- **Interruptor Cliente/Negocio mejorado**: ahora tiene íconos (persona/tienda),
  una píldora deslizante animada y mayor contraste sobre la barra oscura.
- **Íconos reales por categoría** en "Compra por categoría" (antes todas mostraban
  el mismo ícono de canasta).

## Archivos entregados

1. **`superette-central-demo.html`** — el build autocontenido. Doble clic y abre en cualquier navegador. Este es el archivo que se sube a GitHub Pages.
2. **`superette-central-fuente.zip`** — el código fuente completo (sin `node_modules`).
3. Este archivo (`LEEME.md`).

## Cómo desplegarlo en GitHub Pages

No hay conector de GitHub activo en esta sesión, así que el despliegue se hace manualmente:

1. Crea un repositorio público nuevo en `github.com/new`.
2. Ve a **Settings → Pages → Deploy from a branch → `main` / `(root)`**.
3. Sube `superette-central-demo.html` con **Add file → Upload files**, y renómbralo a `index.html` al subirlo (GitHub Pages solo sirve `index.html` como página principal).
4. Espera 1–2 minutos y verifica en `https://tu-usuario.github.io/tu-repo/`.

Una vez desplegado, el código QR en **Negocio → Canales** apunta automáticamente
a la URL real donde esté alojado (se genera con la URL del navegador en el
momento, no está hardcodeado) — así que funciona apenas lo subas, sin tocar código.

## Mapa de las dos modalidades

**Modo Cliente:** Inicio · Compra (catálogo) · Promociones · Carrito · Confirmar compra · Seguimiento de pedido · Mis pedidos · Alertas · Cuenta · Eventos.

**Modo Negocio:** Resumen · Operación (Empaque) · Catálogo · Promociones · Clientes · Canales · Configuración.

El interruptor Cliente/Negocio está en la barra oscura de arriba.

## Guion de presentación (5 pasos)

También está en el modal de Guía (ícono de interrogación en la barra de demo).

1. **Negocio → Canales.** De dónde ya viene la gente: la publicación de Instagram y el QR real. Escanéalo con tu celular en la reunión.
2. **Cliente.** Agrega un producto o una promoción, personalízalo (peso, extras), confirma. Termina en la pantalla de sello con el número de pedido.
3. **Negocio → Empaque.** El pedido aparece marcado como nuevo. Avánzalo dos pasos con un toque.
4. **Cliente → Alertas.** Los avisos ya cambiaron solos y se ven en la simulación de pantalla de bloqueo. **Este es el momento que vende.**
5. **Negocio → Resumen.** Trabajo del día, ventas, top productos. Cierra apagando un producto agotado en Catálogo y copiando el enlace de una promoción para Instagram.

## Antes de presentarlo a un cliente específico

Esto es lo primero que hay que cambiar por cada superette real:

- **`src/data/config.js`** — nombre exacto del negocio (con acentos), pueblo, dirección, teléfono, redes, horario.
- **`src/data/catalogo.js`** — el catálogo real del negocio: productos, precios, categorías.
- **`src/data/promos.js`** — las promociones reales que quiera correr.
- **Fotos** — todas las fotos son de Pexels (libres de derechos) elegidas para lucir como una superette puertorriqueña. Sustitúyelas por fotos reales del negocio (fachada, productos, carnicería) apenas el cliente acepte la propuesta — es lo que más credibilidad le da al portal.
- **Paleta de colores** — está en `src/index.css` (`@theme`). Si el negocio tiene logo o identidad visual propia, ajusta ahí los tokens `--color-verde-*` y `--color-naranja-*`.

## Checklist antes de presentar

- [ ] Botón **Reiniciar** (barra de demo) vuelve todo a su estado inicial
- [ ] Recorrido de 5 pasos probado de punta a punta
- [ ] Probado en el celular real que se usará en la reunión (no solo en la laptop)
- [ ] Nombre del negocio y pueblo correctos si ya es para un cliente específico

## Notas técnicas (por si necesitas tocar el código)

- Stack: Vite + React + Tailwind 4 + `HashRouter` (obligatorio para GitHub Pages) + `vite-plugin-singlefile` (todo se empaqueta en un solo `index.html`).
- Estado: `Context + useReducer` en `src/store/DemoStore.jsx`, con persistencia en `localStorage`. Los dos modos leen y escriben el mismo estado — por eso se ve en vivo.
- Precios: módulo puro en `src/store/pricing.js`, sin React — ahí está toda la aritmética de dinero (subtotal, descuento, IVU 11.5%, cargo de entrega, puntos).
- Todo dato editable tiene un comentario `⚠️ DATOS DE EJEMPLO` al inicio del archivo en `src/data/`.
