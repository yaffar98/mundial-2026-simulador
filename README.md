# Mundial 2026 - Simulador familiar

Esta carpeta contiene una pagina local lista para abrir con doble clic:

`C:\Users\yaffa\Desktop\FOOTBALL\index.html`

La app esta hecha en HTML, CSS y JavaScript puro. El archivo principal es autocontenido para que funcione aunque no haya servidor.

## Archivos

- `index.html`: aplicacion completa.
- `data/worldcup.json`: datos locales que puede editar manualmente.
- `styles.css`: reservado para separar estilos despues.
- `app.js`: reservado para separar JavaScript despues.
- `README.md`: esta guia.

## Modo en vivo

La pagina intenta actualizar datos en vivo por defecto usando la API publica:

`https://worldcup26.ir`

No necesita API key para esa fuente. Consulta:

- `https://worldcup26.ir/get/games`
- `https://worldcup26.ir/get/groups`
- `https://worldcup26.ir/get/teams`

La actualizacion automatica queda cada 2 minutos. Si esa fuente falla, la app usa `data/worldcup.json` y luego la copia interna.

## API key opcional

Si quiere usar otra API, cree un archivo llamado `config.js` junto a `index.html`.

WorldCup26 publico:

```js
window.WORLD_CUP_CONFIG = {
  provider: "worldcup26",
  endpointBase: "https://worldcup26.ir",
  autoRefreshMinutes: 2
};
```

API-FOOTBALL / API-SPORTS:

```js
window.WORLD_CUP_CONFIG = {
  provider: "api-football",
  apiKey: "TU_API_KEY",
  season: 2026,
  leagueId: 1,
  autoRefreshMinutes: 5
};
```

football-data.org:

```js
window.WORLD_CUP_CONFIG = {
  provider: "football-data",
  apiKey: "TU_API_KEY",
  competition: "WC",
  autoRefreshMinutes: 5
};
```

Sportmonks:

```js
window.WORLD_CUP_CONFIG = {
  provider: "sportmonks",
  apiKey: "TU_API_KEY",
  seasonId: "WORLD_CUP_2026",
  autoRefreshMinutes: 5
};
```

Si no existe `config.js`, la app intenta leer `data/worldcup.json`. Si el navegador bloquea esa lectura por abrir con doble clic, usa una copia interna de datos para que la pagina no se rompa.

## Actualizacion automatica

La pagina se actualiza sola cada 2 minutos. Puede cambiarlo en `config.js` con:

```js
autoRefreshMinutes: 2
```

Tambien se vuelve a actualizar cuando regresa a la pestaña despues de dejarla abierta. Si la API falla, conserva los datos que ya tenia y muestra: `No se pudo actualizar en linea, usando datos guardados.`

## Reglas de uso

- Los partidos con estado `REAL` o `LIVE` no se pueden modificar.
- Los partidos `PENDING` se pueden simular.
- Las simulaciones se guardan en `localStorage` de esta computadora.
- El boton `Restablecer simulacion` borra lo simulado.
- El boton `Usar resultados reales disponibles` vuelve a la base local/API sin simulaciones.

## Estados

- `REAL`: resultado final bloqueado.
- `LIVE`: partido en vivo bloqueado.
- `PENDING`: pendiente, se puede simular.
- `SIMULATED`: resultado escogido por el usuario.

## Fuentes de referencia

- FIFA: calendario y resultados oficiales del Mundial 2026.
- LiveScore: grupos y formato de 12 grupos, dos primeros y ocho mejores terceros.
- API-FOOTBALL/API-SPORTS, football-data.org y Sportmonks: opciones preparadas para datos en linea.
