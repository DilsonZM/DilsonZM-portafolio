# Dilson Zuleta — Portfolio Premium

> Landing page profesional de alto impacto. Sitio estático HTML/CSS/JS sin frameworks ni build tools.

## Visión general

Portfolio personal premium para **Dilson Zuleta** — Analista de Datos, Desarrollador Full Stack y Especialista en Automatización. Diseño dark theme tecnológico con estética similar a Vercel/Stripe, animaciones cuidadas y excelente UX/UI.

**Stack:** HTML5 + CSS3 puro + JavaScript vanilla  
**Dependencias externas:** Google Fonts (Inter + JetBrains Mono)  
**Hosting:** GitHub Pages (rama `main`, carpeta raíz `/`)

## Estructura del proyecto

```
/
├── index.html          # Página única con 9 secciones
├── styles.css          # Sistema de diseño completo (~2000 líneas)
├── script.js           # Módulos de interacción y animaciones
├── AGENTS.md           # Este archivo
└── .github/            # Configuración de GitHub
```

## Convenciones de código

### CSS — BEM estricto

```css
/* Bloque */
.nav { }
/* Elemento */
.nav__container { }
.nav__link { }
/* Modificador */
.nav__link--cta { }
.btn--primary { }
.projects__card--featured { }
```

### Variables CSS (design tokens)

Todas las variables están en `:root` en `styles.css`. **Nunca hardcodear colores, espaciados o radios** — usar siempre las variables:

| Categoría | Tokens clave |
|---|---|
| Fondos | `--bg-primary`, `--bg-secondary`, `--bg-surface`, `--bg-elevated` |
| Bordes | `--border-subtle`, `--border-medium`, `--border-strong` |
| Texto | `--text-primary`, `--text-secondary`, `--text-muted` |
| Acento | `--accent`, `--accent-light`, `--accent-dark`, `--accent-gradient` |
| Transiciones | `--ease-out-expo`, `--ease-out-quart` |
| Radios | `--radius-sm` (6px) → `--radius-full` (9999px) |
| Sombras | `--shadow-sm`, `--shadow-md`, `--shadow-lg`, `--shadow-glow` |

### Paleta de colores

- **Fondo base:** `#050505` (casi negro)
- **Superficie:** `#111113`
- **Acento:** `#22d3ee` (cyan)
- **Gradiente acento:** cyan → blue → purple
- Secciones alternan `--bg-primary` ↔ `--bg-secondary` con línea gradiente superior

### HTML — Patrón de sección estándar

```html
<section class="section" id="section">
  <div class="container">
    <div class="section-header reveal-up">
      <span class="section-tag">Etiqueta</span>
      <h2 class="section-title">Título con <span class="accent">acento</span></h2>
      <p class="section-subtitle">Subtítulo opcional</p>
    </div>
    <!-- contenido -->
  </div>
</section>
```

### Animaciones — Scroll reveal

```html
<!-- Clases de reveal + delay vía CSS custom property -->
<div class="reveal-up" style="--delay: 0.1s">...</div>
<div class="reveal-left">...</div>
<div class="reveal-right">...</div>
```

Las animaciones se activan al entrar en viewport con IntersectionObserver. Respetan `prefers-reduced-motion`.

### JavaScript — Módulos independientes

Cada funcionalidad está en su propia función `init*()`, todas llamadas desde `DOMContentLoaded`:

```js
document.addEventListener('DOMContentLoaded', () => {
    initCursorGlow();
    initNavigation();
    initHeroCanvas();
    initScrollReveal();
    // ...
});
```

No hay estado global compartido entre módulos.

## Secciones de la página

1. **Hero** — Canvas de partículas interactivo, headline con gradient text, badge de disponibilidad, métricas animadas, doble CTA
2. **Sobre mí** — Split layout: bloque de código + tarjetas flotantes / texto profesional
3. **Habilidades** — 3 categorías con barras animadas + marquee infinito de tecnologías
4. **Proyectos** — 7 proyectos en bento grid con storytelling, tecnologías e impacto medible
5. **Trayectoria** — Timeline vertical con hover effects + panel de métricas
6. **Formación** — 6 certificaciones en grid con iconos
7. **Fortalezas** — 8 cards numeradas
8. **Testimonios** — Carrusel con auto-play, controles y swipe táctil
9. **Contacto** — CTA con glow de fondo, enlaces a email y LinkedIn

## Breakpoints responsivos

| Breakpoint | Cambios |
|---|---|
| `≤1024px` | Skills/projects 1 columna, strengths/education 2 columnas |
| `≤768px` | Nav → hamburger, hero compacto, about 1 columna |
| `≤480px` | Botones full-width, CTAs apiladas, impact metrics 1 columna |

## Información del perfil

- **Nombre:** Dilson Zuleta
- **Rol:** Analista de Datos · Desarrollador Full Stack · Especialista en Automatización
- **Ubicación:** Colombia · Disponible remoto global
- **Email:** dilson.zuleta@email.com
- **LinkedIn:** linkedin.com/in/dilsonzuleta
- **Idioma:** Todo el contenido está en español

## Despliegue

- **Plataforma:** GitHub Pages
- **Rama:** `main`
- **Carpeta raíz:** `/` (root)
- **URL pública:** https://dilsonzm.github.io/DilsonZM-portafolio/

## Pitfalls conocidos

- Google Fonts requiere conexión a internet — sin CDN no se cargan las fuentes (se usa fallback system font)
- Canvas de partículas consume recursos en dispositivos antiguos — `prefers-reduced-motion` desactiva las animaciones CSS pero el canvas sigue corriendo
- El carrusel de testimonios no tiene lazy loading de contenido
