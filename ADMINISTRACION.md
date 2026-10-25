# DOGI COFFEE — administración del menú

## Menú público

La página principal carga los productos desde `content/productos/*.json`. Cada producto usa estos campos:

- `id`: identificador estable.
- `title`: nombre visible.
- `category`: Cafés Calientes, Bebidas Frías, Especialidades o Snacks.
- `price`: precio en MXN (número).
- `description`: descripción.
- `image`: URL o ruta de la imagen.

Para cambios manuales, puedes editar los archivos JSON desde GitHub. Los cambios aparecen en el menú cuando GitHub Pages termina de publicar el sitio.

## Panel de administración (`/admin/`)

El panel usa Decap CMS, pero **el inicio de sesión aún necesita configurarse**. GitHub Pages solo publica archivos estáticos y no puede guardar cambios autenticados en el repositorio por sí solo. La configuración antigua `git-gateway` depende de Netlify Identity/Git Gateway y no funcionará solo por subir la página a GitHub Pages.

Para habilitar la edición visual de forma segura hay que configurar un proveedor OAuth compatible con Decap CMS y conectar el backend `github` al repositorio `giovanniFT27/dogi-coffee`. Esto requiere una URL del servicio OAuth y sus secretos guardados en el servidor/proveedor, **nunca en JavaScript público ni dentro de este repositorio**. No introduzcas un token personal de GitHub en el navegador.

Una vez elegido y configurado el proveedor OAuth, se actualizará `admin/config.yml` con su URL real y se probará el flujo de inicio de sesión antes de considerar listo el panel.

## Imágenes

El CMS está preparado para guardar imágenes en `assets/images`. Conviene verificar la ruta pública de imágenes según la URL final de GitHub Pages (URL de proyecto o dominio propio) antes de cargar muchas imágenes.
