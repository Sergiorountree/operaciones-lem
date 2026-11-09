# Portal operaciones.grupolem.com — reglas para Claude en este repositorio

Este repositorio es el **front estático** del portal de Grupo LEM. GitHub Pages publica la rama `main` en
`operaciones.grupolem.com`: lo que entra a `main` está en producción en minutos.

**El repositorio es público.** Todo lo que se escriba aquí lo puede leer cualquiera.

## Qué hay aquí

| Ruta | Qué es |
|---|---|
| `index.html` | Lanzador del portal |
| `compras/`, `inventarios/`, `nominas/`, `ventas/`, `contabilidad/`, `asistente/` | Un módulo por carpeta, cada uno en un solo `index.html` |
| `punto-de-vista.js` | Código común de "Ver como"; lo cargan todas las páginas |
| `CNAME` | Dominio de Pages. No se toca |

Cada página habla con el servidor con su función `api(accion, datos)`. Los permisos, los datos y los cálculos viven
en el servidor, no en el navegador.

## Qué se puede cambiar desde aquí y qué no

**Sí:** HTML, CSS y JavaScript de las páginas (textos, estilos, etiquetas, validaciones de captura, cómo se presenta
algo que el servidor ya entrega).

**No, nunca desde este repositorio:** base de datos, migraciones, acciones nuevas de la API, reglas de permisos,
Firebase, n8n. Eso vive fuera de este repositorio y lo aplican personas autorizadas.

Si un cambio necesita un dato o una acción que el servidor todavía no entrega:

1. No inventes la acción ni simules el dato en el navegador.
2. Escribe en el issue o en el PR qué acción hace falta, con qué campos de entrada y de salida.
3. Detente ahí y marca el PR o el issue como **"requiere cambio de servidor"**.

## Lo que nunca se escribe en este repositorio

- Contraseñas, llaves, tokens, cadenas de conexión o cualquier secreto.
- SQL de migraciones o de consultas internas.
- Nombres, correos, sueldos o cualquier dato personal de colaboradores; montos reales del negocio.
- Capturas de pantalla o ejemplos con datos reales. Los ejemplos usan datos ficticios.

Los identificadores públicos que ya están en las páginas (cliente OAuth, configuración web de Firebase) se quedan
como están; no se agregan otros.

## Cómo se trabaja

- **Nunca se hace commit directo a `main`.** Todo cambio va en una rama y en un pull request.
- **Un ticket, un PR, un módulo.** El PR toca solo los archivos del módulo del ticket.
- **Diffs mínimos.** Las páginas son archivos únicos de 20 a 260 KB: no reformatees, no reordenes, no renombres ni
  "limpies" código que el ticket no pide. Cambia solo las líneas necesarias.
- **Riesgo alto, solo si el ticket lo pide de forma explícita:** `punto-de-vista.js`, el inicio de sesión, la función
  `api()` y cualquier cosa que toque permisos, dinero o nómina. Si el cambio cae ahí, dilo en la primera línea del PR.
- **No cambies el sistema visual de un módulo dentro de un ticket.** Respeta los estilos que el módulo ya usa.
- Textos de pantalla y comentarios en español. Un cambio no obvio lleva un comentario corto con la fecha y el motivo.
- Si el ticket contradice una regla de este archivo o no se entiende, no decidas: pregunta en el issue.

## Reglas de las pantallas

- El módulo va centrado, a 1320 px de ancho.
- Toda acción que guarda pide confirmación en un modal antes de mandar.
- Las tablas de captura del administrador no llevan spinners y usan el aspecto de `.hoja`.
- Donde haya `.btn` con flex, los elementos ocultos necesitan `[hidden]{display:none!important}`.
- Una pantalla que sustituye a una app se copia del diseño de esa app; no se inventa.
- **Los números los calcula el servidor.** El navegador presenta; no recalcula cifras de negocio.
- La fecha "de hoy" para reglas de negocio la da el servidor, no el reloj del navegador.
- Si cambias `punto-de-vista.js`, sube el número de versión con el que lo cargan las páginas (`?v=`).

## Cómo se describe un PR

1. **Qué cambió**, en dos o tres líneas, y el ticket al que responde.
2. **Cómo probarlo:** pantalla, pasos y qué se debe ver.
3. **Riesgo:** bajo o alto, y por qué.
4. **¿Requiere cambio de servidor?** Sí o no; si sí, qué acción y qué campos.

## Publicación y prueba

- Publicar es mergear a `main`, y eso lo hace una persona autorizada. Claude no mergea.
- Pages guarda las páginas en caché unos 10 minutos; después de publicar se recarga con Cmd+Shift+R.
- El inicio de sesión con Google no se automatiza: la prueba funcional la hace una persona con su cuenta.
