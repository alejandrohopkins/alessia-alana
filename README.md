# Plan de estudio — Alana y Alessia

Sitio estático. Tres archivos, sin build ni dependencias.

```
index.html     → página de inicio
alana.html     → dashboard de Alana
alessia.html   → dashboard de Alessia
```

## Publicar en Vercel

1. Entra a https://vercel.com/new
2. Arrastra los tres archivos (o la carpeta que los contiene)
3. Framework preset: **Other**. Build command y output directory: vacíos
4. Deploy

URLs resultantes:
- `tusitio.vercel.app` → inicio
- `tusitio.vercel.app/alana.html`
- `tusitio.vercel.app/alessia.html`

## Probar antes de publicar

Abre `index.html` directamente en el navegador con doble click. Funciona igual
que publicado — el guardado de progreso también.

## Cómo se guarda el progreso

Con `localStorage`. Cada una marca sus bloques y al volver siguen marcados.
Sin login ni cuenta.

Límite importante: **el progreso vive en ese navegador y en esa computadora.**
Si usa la laptop y luego el iPad, son dos progresos separados.

El botón "Copiar resumen para papá" arma un texto con el avance y lo copia
al portapapeles para pegarlo en WhatsApp.

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
