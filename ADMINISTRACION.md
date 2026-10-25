# DOGI COFFEE — menú y panel administrativo

## Menú público

La página principal lee los productos de `content/productos/*.json`. Cada producto tiene:

- `id`: identificador.
- `title`: nombre.
- `category`: Cafés Calientes, Bebidas Frías, Especialidades o Snacks.
- `price`: precio numérico en MXN.
- `description`: descripción.
- `image`: URL o ruta de imagen.

Los productos iniciales ya están guardados en `content/productos/`. Cuando GitHub Pages termine de publicar los cambios, el menú público los leerá desde ahí.

## Panel administrativo

La dirección del panel será la URL del sitio seguida de `/admin/`. Por ejemplo, si el sitio es `https://giovanniFT27.github.io/dogi-coffee/`, el panel estará en `https://giovanniFT27.github.io/dogi-coffee/admin/`.

**Importante:** el panel todavía no está listo para iniciar sesión. GitHub Pages solo sirve archivos estáticos y no autentica editores ni puede guardar cambios privados en GitHub por sí solo. La configuración antigua `git-gateway` depende de Netlify Identity/Git Gateway, que no se activa por alojar el sitio en GitHub Pages.

### Opción recomendada: GitHub + Cloudflare Worker (plan gratuito)

Decap CMS admite el backend GitHub y necesita un servicio OAuth para completar el inicio de sesión. Un Worker puede tener su propia URL gratuita `*.workers.dev`, así que no necesitas comprar un dominio.

1. Crea una cuenta gratuita en [Cloudflare](https://dash.cloudflare.com/sign-up).
2. Crea un repositorio propio a partir de la plantilla [Decap CMS GitHub OAuth Provider para Cloudflare](https://github.com/ottmartens/decap-cms-github-oauth-provider-cloudflare). Sigue las instrucciones de su README para desplegar el Worker. También puedes usar el método de despliegue con Wrangler descrito por la plantilla.
3. En GitHub, abre **Settings → Developer settings → OAuth Apps → New OAuth App**. Usa como **Homepage URL** la URL pública de DOGI COFFEE. Como **Authorization callback URL**, usa la URL de tu Worker seguida de `/callback` (consulta el README de la plantilla para confirmar la ruta exacta).
4. Copia el Client ID y genera un Client Secret. Configura ambos como secretos del Worker/Cloudflare, siguiendo el README de la plantilla. **No publiques el Client Secret ni un token personal de GitHub en este repositorio, en el menú, ni en el navegador.**
5. Cuando el Worker esté desplegado, tendrás una URL parecida a `https://nombre-del-worker.tu-cuenta.workers.dev`. Esa URL real es la que se debe colocar como `backend.base_url` en `admin/config.yml`, usando el backend `github` y el repositorio `giovanniFT27/dogi-coffee`.
6. En la configuración de la OAuth App, asegúrate de usar la URL de callback que requiere exactamente la plantilla desplegada. La autenticación debe probarse antes de dar el panel por terminado.

La plantilla y sus instrucciones son importantes porque la ruta de callback puede variar según el proyecto OAuth utilizado. No uses una URL de ejemplo o inventada.

### Quién puede editar

Para que el backend GitHub de Decap CMS pueda guardar cambios, el usuario que inicie sesión debe tener permiso de escritura en el repositorio. Protege el acceso concediendo ese permiso únicamente a la cuenta administradora que quieras autorizar.

## Imágenes de productos

El CMS está configurado para guardar imágenes en `assets/images`. Antes de subir imágenes desde el panel, hay que ajustar `public_folder` a la ruta pública real del sitio de GitHub Pages, que normalmente incluye `/dogi-coffee/` porque es un sitio de proyecto. Después hay que probar que las imágenes cargadas se vean en la página pública.
