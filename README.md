# AYNI English Library

Biblioteca digital de libros en inglés de la IE Nuestra Señora del Pilar.

## Estructura

```
AYNI/
├── index.html      # Sitio público (catálogo + collage de portadas)
├── admin.html      # Panel de administración (contraseña: 0000)
├── data/
│   └── books.json  # Respaldo del catálogo (solo se usa si la nube falla)
├── covers/         # Carpeta opcional para imágenes sueltas
├── logo.png
└── manifest.json
```

## Publicar un libro (automático)

1. Abre `admin.html` e introduce la contraseña `####`.
2. Crea o edita el libro y sube su portada.
3. Pulsa **Guardar Libro**.

Eso es todo. El libro se guarda en la nube y aparece en el sitio al instante. No hay que descargar ni reemplazar archivos.

- **Portadas:** se optimizan (máx. 700 px, JPEG) y se suben a ImgBB.
- **Catálogo:** se guarda en JSONBin y el sitio lo lee sin caché.
- El sitio se refresca solo al volver a la pestaña y cada 60 segundos.
- `data/books.json` es solo un respaldo: si la nube no responde, se muestra ese archivo.

## Notas

- La contraseña del panel es una protección básica del lado del cliente. Para seguridad real conviene proteger `/admin.html` con Netlify (password protection) o reglas de acceso.
- Las claves de JSONBin e ImgBB están en el código del panel. No compartas el enlace del admin públicamente.
- Para migrar a un almacenamiento propio (sin servicios externos) se puede usar Supabase o Netlify Blobs.
