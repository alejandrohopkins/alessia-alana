# Plan de estudio — Alana y Alessia

Sitio estático. Cuatro archivos, sin build ni dependencias (salvo un
proyecto de Supabase gratuito para el reporte online — ver abajo).

```
index.html     → página de inicio
alana.html     → dashboard de Alana
alessia.html   → dashboard de Alessia
papa.html      → reporte online para papá (lee de Supabase)
```

## Publicar en Vercel

1. Entra a https://vercel.com/new
2. Arrastra los cuatro archivos (o la carpeta que los contiene)
3. Framework preset: **Other**. Build command y output directory: vacíos
4. Deploy

URLs resultantes:
- `tusitio.vercel.app` → inicio
- `tusitio.vercel.app/alana.html`
- `tusitio.vercel.app/alessia.html`
- `tusitio.vercel.app/papa.html`

## Probar antes de publicar

Abre `index.html` directamente en el navegador con doble click. Funciona igual
que publicado — el guardado de progreso también.

## Cómo se guarda el progreso

Con `localStorage`. Cada una marca sus bloques y al volver siguen marcados.
Sin login ni cuenta.

Límite importante: **el progreso vive en ese navegador y en esa computadora.**
Si usa la laptop y luego el iPad, son dos progresos separados.

El botón "Copiar resumen para papá" arma un texto con el avance y lo copia
al portapapeles para pegarlo en WhatsApp — sigue funcionando igual que antes.

## Reporte online para papá (`papa.html`)

Cada vez que Alana o Alessia marcan un bloque, una unidad de Khan, o escriben
un entregable, la página manda ese evento (además de guardarlo en
`localStorage` como siempre) a una tabla `activity_log` en Supabase, usando
la clave pública ("anon") del proyecto. `papa.html` lee esa misma tabla y
muestra, agrupado por fecha real, qué hizo cada una — sin que ellas tengan
que hacer nada aparte de usar su página normalmente.

**Privacidad:** `papa.html` no tiene contraseña. Cualquiera con el link (y la
clave pública, visible en el código fuente) puede leer la tabla. Es el mismo
nivel de privacidad que ya tenía el sitio (sin login) — no compartas ese link
fuera de la familia. Si más adelante querés protegerlo con contraseña, se
puede agregar.

Proyecto de Supabase: `alessia-alana-progreso` (organización DOSA). Tablas:
- `activity_log`: cada acción registrada (qué, cuándo, de quién).
- `feedback`: las correcciones que escribe la rutina diaria (ver abajo).

## Corrección automática al final del día

Hay una Rutina programada ("Revisión diaria — Alana y Alessia") que corre
todos los días a las 8pm hora de Panamá. Lee lo que se hizo en las últimas
horas, corrige los entregables de texto contra la tarea del día (usando
`PROJECTS`/`SAT` de cada HTML como rúbrica), guarda su corrección en la
tabla `feedback` de Supabase (visible en `papa.html`, debajo de cada
entregable), y manda un resumen corto por correo y notificación push a la
cuenta que la creó. Se puede editar el horario o desactivarla desde la lista
de Rutinas de Claude Code.

## Cambiar el contenido

El temario vive en la variable `DATA` dentro de cada HTML:

```js
DATA = {
  1: {                          // número de semana
    Lun: {
      hrs: '4 horas',
      blocks: [
        {
          t: '9:00–10:00',      // horario
          s: 'Math — ...',      // materia y título
          d: 'Descripción...',  // qué hacer
          a: 1,                 // opcional: 1 = bloque de tarde
          l: [['Etiqueta','https://url']]   // opcional: links
        }
      ]
    }
  }
}
```

Para agregar la semana 3: copia el bloque `2:`, edítalo como `3:`, y agrega
un botón `<button data-w="3">Semana 3</button>` en el selector de semanas.
