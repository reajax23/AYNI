# AYNI English Library — Resumen de Cambios

**Fecha**: 2026-11-06  
**Para**: Ms. Jenny Alvarado (Project Leader / Profesora de inglés)  
**Proyecto**: AYNI English Library — IE Nuestra Señora del Pilar, Bucaramanga

---

## 📋 Cambios Implementados

### 1. Sitio Público (`index.html`)

| Área | Cambio |
|------|--------|
| **Idioma por defecto** | Inglés (`lang='en'`) al abrir; botón EN/ES en cabecera |
| **Botón Admin (⚙)** | Movido a **esquina inferior izquierda** (era derecha) |
| **Header escuela** | ES: `IE Nuestra Señora del Pilar` / EN: `SCHOOL Nuestra Señora del Pilar` (vía I18N) |
| **Footer** | `Project Leader: Jenny Alvarado`<br>`E-mail: aynienglishlibrary@gmail.com` (sin "Bucaramanga, Colombia") |
| **Sidebar "Sobre el Proyecto"** | 5 pestañas con contenido de `info.odt`:<br>1. 📖 ¿Qué es? / What is AYNI?<br>2. 🎯 Misión / Mission<br>3. 🌟 Visión / Vision<br>4. 💡 Cómo funciona / How it works (lista 1-5)<br>5. 👩‍🏫 Espacio Docentes / Teacher's Corner (contacto email) |
| **Copyright** | Texto `© 2026 Ayni English Library...` → **click despliega dropdown** con aviso legal completo |
| **Catálogo** | 10 libros/página (era 8) |
| **Categorías dinámicas** | Se leen de `localStorage['ayni_categories']` (sync automático con admin) |
| **Espacio inferior** | `padding-bottom: 5rem` en `.info-sidebar__content` para marca de agua Netlify |
| **Auto-refresh** | Cada 60s y al volver a la pestaña (`visibilitychange`) |

---

### 2. Panel Admin (`admin.html`)

| Función | Detalle |
|---------|---------|
| **Login** | Contraseña: `@Ayni1984` |
| **Toggle ver/ocultar** | Botón 👁️ / 🙈 en campo contraseña |
| **Cookie persistente** | `ayni_admin_auth=1` por **365 días**, `SameSite=Lax`, path `/` |
| **Gestión categorías** | Modal 🏷️: Añadir / Editar / Eliminar (valor + etiqueta visible). Guarda en `localStorage` |
| **Subida imágenes** | • Timeout 30s con `AbortController`<br>• Validación MIME + límite 10MB<br>• Compresión JPEG 82% / máx. 700px<br>• **Fallback base64 local** si ImgBB falla (badge "⚠️ Local" vs "✅ En la nube") |
| **Exportar/Importar** | Botones en cabecera para respaldo JSON manual |
| **Espacio inferior** | `padding-bottom: 5rem` en `.layout` para marca de agua Netlify |

---

### 3. Arquitectura Técnica

- **Cloud-first**: JSONBin.io (catálogo) + ImgBB (portadas)
- **Fallback local**: `data/books.json` + `localStorage` si falla la nube
- **PWA ready**: `manifest.json` + Service Worker (`sw.js`)
- **Despliegue**: Netlify (scripts HUD incluidos)
- **Categorías sync**: Admin escribe `localStorage` → Sitio público lo lee al cargar

---

### 4. Archivos Modificados

```
/home/thc/Documentos/AYNI/
├── index.html          # Sitio público (57.9 KB)
├── admin.html          # Panel admin (41.8 KB)
├── data/books.json     # Backup local catálogo (4.1 KB)
├── info.odt            # Fuente textos sidebar (36.9 KB)
├── README.md           # Documentación
├── logo.png            # Logo
├── manifest.json       # PWA manifest
└── CHANGES_SUMMARY.md  # Este archivo
```

---

### 5. Seguridad / Notas para Producción

⚠️ **Actual**: Claves JSONBin/ImgBB en código cliente (OK para uso escolar interno)  
🔒 **Producción real**: Proteger `/admin.html` con **Netlify Password Protection** o migrar a **Supabase / Netlify Blobs**  
🍪 Cookie admin: `SameSite=Lax`, 365 días, solo HTTPS en producción

---

### 6. Cómo Probar

```bash
# Abrir sitio público
open /home/thc/Documentos/AYNI/index.html

# Abrir admin (modo incógnito para forzar login)
# Contraseña: @Ayni1984
open /home/thc/Documentos/AYNI/admin.html
```

---

**Contacto**: aynienglishlibrary@gmail.com  
**Project Leader**: Jenny Alvarado