# Portal operaciones.grupolem.com — reglas para agentes

Este repositorio es el front estático del portal de Grupo LEM. GitHub Pages publica la rama `main` en
`operaciones.grupolem.com`: lo que entra a `main` está en producción en minutos. **El repositorio es público.**

Las reglas completas están en `.claude/CLAUDE.md` y valen para cualquier agente. Este archivo las resume para la
revisión de pull requests. Si los dos archivos se contradicen, manda `.claude/CLAUDE.md` y se avisa en el PR.

- Los agentes no hacen merge ni push a `main`. Publicar lo hace una persona autorizada.
- Los comentarios de revisión se escriben en español, cortos y con la línea exacta.

## Code Review Rules

### Secretos y datos

- Marca cualquier contraseña, llave, token o cadena de conexión que aparezca en el diff. Los identificadores públicos
  que ya estaban en las páginas (cliente OAuth, configuración web de Firebase) se quedan; no se agregan otros.
- Marca nombres, correos o sueldos de colaboradores, montos reales del negocio y ejemplos con datos reales. Los
  ejemplos usan datos ficticios.
- Marca SQL de migraciones o de consultas internas: no vive en este repositorio.

### Alcance del cambio

- Un PR toca un solo módulo (`compras/`, `inventarios/`, `nominas/`, `ventas/`, `contabilidad/`, `asistente/` o el
  lanzador `index.html`). Marca archivos de otro módulo que el ticket no pide.
- Las páginas son archivos únicos de 20 a 260 KB. Marca reformateos, reordenamientos, renombres o "limpiezas" que el
  ticket no pide: el diff debe traer solo las líneas necesarias.
- Riesgo alto: `punto-de-vista.js`, el inicio de sesión, la función `api()` y cualquier cosa que toque permisos, dinero
  o nómina. Si el diff cae ahí, la primera línea del PR debe decirlo; si no lo dice, márcalo.
- `CNAME` no se toca.

### Servidor

- Los permisos, los datos y los cálculos viven en el servidor. Marca cifras de negocio recalculadas en el navegador,
  datos simulados y llamadas a acciones de `api()` que el servidor no entrega.
- La fecha "de hoy" para reglas de negocio la da el servidor. Marca reglas que dependan del reloj del navegador.
- Si el cambio necesita una acción o un dato nuevo del servidor, el PR debe decir "requiere cambio de servidor" con
  los campos de entrada y de salida.

### Pantallas

- Toda acción que guarda pide confirmación en un modal antes de mandar.
- Donde haya `.btn` con flex, los elementos ocultos necesitan `[hidden]{display:none!important}`.
- Un ticket no cambia el sistema visual del módulo. Textos de pantalla y comentarios van en español.
- Si cambia `punto-de-vista.js`, las páginas deben cargarlo con un `?v=` nuevo.

### Qué no revisar

- Estilo, formato y preferencias de nombres en código que el PR no tocó.
- El inicio de sesión con Google no se puede probar en automático: esa prueba la hace una persona.
