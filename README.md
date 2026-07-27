# Plan de estudio — Alana y Alessia

Sitio estático. Sin build, sin dependencias, sin backend.

## Estructura

```
/
  index.html          → página de inicio (elegir quién eres)
  alana/index.html    → dashboard de Alana      → /alana
  alessia/index.html  → dashboard de Alessia    → /alessia
```

## Cómo publicar en Vercel

**Opción A — arrastrar la carpeta (más rápido)**

1. Entra a https://vercel.com/new
2. Arrastra esta carpeta completa a la zona de drop
3. Vercel detecta que es un sitio estático y publica
4. Te da una URL tipo `plan-estudio.vercel.app`

**Opción B — desde GitHub**

1. Sube esta carpeta a un repo
2. En Vercel: New Project → importa el repo
3. Framework preset: **Other**
4. Build command: dejar vacío
5. Output directory: dejar vacío (o `.`)
6. Deploy

## Dominio propio

Si tienes un dominio, en Vercel: Project → Settings → Domains → agregar.
Puedes usar un subdominio, por ejemplo `estudio.tudominio.com`.

## Cómo se guarda el progreso

Con `localStorage` del navegador. Esto significa:

- Cada una marca sus bloques y al volver siguen marcados
- No hace falta login ni cuenta
- **El progreso vive en ese navegador y en esa computadora.** Si usa la laptop
  y luego el iPad, son dos progresos distintos
- Si borran datos del navegador, se pierde
- El botón "Copiar resumen para papá" arma un texto con el avance y lo copia
  al portapapeles para pegarlo en WhatsApp

## Cambiar el contenido

Todo el temario vive en la variable `DATA` dentro de cada archivo HTML.
La estructura es:

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

Para agregar la semana 3, copia el bloque `2:` y edítalo como `3:`, y agrega
`3` al selector de semanas en el HTML.
