# Nexocorp · Torre de Control de Conciliaciones

Dashboard web (panel ejecutivo, panel operativo y ficha por período) que lee las conciliaciones publicadas en Supabase.
Es una página estática: HTML, CSS y JavaScript, sin instalación ni compilación.

## Archivos

```
index.html               página principal (ingreso + aplicación)
css/estilos.css          estilos
js/config.js             configuración: URL de Supabase, clave pública, plazos de atraso
js/util.js               formato de números y fechas
js/datos.js              lectura de Supabase (con paginación de 1000 filas)
js/calculos.js           calendario de períodos, estados, filtros y totales
js/vista-ejecutivo.js    panel ejecutivo
js/vista-operativo.js    panel operativo
js/vista-ficha.js        ficha de un período
js/app.js                inicio de sesión, filtros y navegación
```

## 1. Pegar la clave pública

1. En Supabase: **Project Settings → API Keys → Publishable key** (empieza con `sb_publishable_`). Cópiala.
2. Abre `js/config.js` y reemplaza `PEGAR_AQUI_LA_CLAVE_PUBLICA` por esa clave.

La clave pública está hecha para ir en el navegador: sin iniciar sesión no permite ver nada (lo impide RLS).
**Nunca** pongas la clave secreta (`sb_secret_...`) en estos archivos.

## 2. Configurar el acceso en Supabase (una sola vez)

1. **Authentication → Sign In / Providers → Email**: activo. Desactiva **Allow new users to sign up** para que nadie pueda crearse una cuenta por su cuenta.
2. **Authentication → Users → Add user → Create new user**: correo y contraseña de cada persona, con **Auto Confirm User** marcado.
3. Cuando tengas la dirección de GitHub Pages: **Authentication → URL Configuration → Site URL** = esa dirección.

## 3. Publicar en GitHub Pages

Opción A, desde la web de GitHub:
1. Crea un repositorio nuevo (público; GitHub Pages gratis lo requiere).
2. **Add file → Upload files** y arrastra **el contenido** de esta carpeta (`index.html` debe quedar en la raíz, junto a las carpetas `css` y `js`). **Commit changes**.
3. **Settings → Pages → Build and deployment**: Source **Deploy from a branch**, rama `main`, carpeta `/ (root)` → **Save**.
4. En uno o dos minutos queda en `https://TU-USUARIO.github.io/NOMBRE-DEL-REPO/`.

Opción B, desde Visual Studio Code: abre esta carpeta (**File → Open Folder**), ve a **Source Control → Publish to GitHub** y elige repositorio público. Luego haz el paso 3 de la opción A.

Para actualizar después: reemplaza los archivos cambiados (subiéndolos de nuevo o con commit y push).

## 4. Probar en tu computadora antes de subir

Abre `index.html` con doble clic en Chrome o Edge, o usa la extensión **Live Server** de VS Code (clic derecho en `index.html` → *Open with Live Server*).

## Ajustes frecuentes (`js/config.js`)

- `cuentas`: fecha desde la que se esperan conciliaciones y días para considerar un período atrasado
  (PedidosYa 7 días, Yango 10 días después del cierre).
- Una cuenta nueva (Turbo, PedidosYa Brands, Yango Brands) aparece sola en filtros, mapa y comparaciones al publicarse
  su primera conciliación; si no la agregas aquí usa los valores por defecto.
- `umbralDescuadreBodega`: diferencia por sucursal (Bs) a partir de la cual se marca para revisar.

## Notas

- El panel solo **lee** datos; no modifica nada en Supabase.
- El repositorio público muestra el código, la URL del proyecto y la clave pública, no los datos:
  los datos solo se ven después de iniciar sesión.
- En la red de la oficina, si aparece "No se pudieron leer los datos", espera unos minutos y pulsa **Reintentar**.
