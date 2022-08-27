# APLICACIÓN DE TAREAS CON SVELTE

# svelte app

Hecho a partir de la plantilla de [Svelte](https://svelte.dev). Más info en: https://github.com/sveltejs/template.

Para crear un nuevo proyecto basado en esta plantilla usando degit / [degit](https://github.com/Rich-Harris/degit):

```bash
npx degit sveltejs/template nombre-app
cd nombre-app
```

_Debes tener una versión de [Node.js](https://nodejs.org) +12.3 instalada._

## Para empezar:

Instalar las dependencias con:

```bash
cd nombre-app
npm install
```

...y después inicializar [Rollup](https://rollupjs.org):

```bash
npm run dev
```

Navegar a [localhost:8080](http://localhost:8080). Para ver la aplicación corriendo, editar los archivos y componentes en `src`, guardar para ver los cambios con el hot reloading.

Por defecto el servidor solo responde llamados del localhost. Para activar la conexión con otros ordenadores, editar el comando `sirv` en el package.json e incluir la opción `--host 0.0.0.0`.

## Modo producción

Para crear una versión "optimizada" de la aplicación ejecutar el siguiente comando:

```bash
npm run build
```

Una vez ejecutado es posible usar `npm run start` para que la aplicación funcione cuando ya haya sido desplegada en plataformas como [Heroku](https://heroku.com).

## Desplegando a la web:

### Con [Vercel](https://vercel.com)

Instalar el CLI `vercel`:

```bash
npm install -g vercel
```

Despues una vez situado en la carpeta del proyecto:

```bash
cd public
vercel deploy --name nombre-app
```

### Con [surge](https://surge.sh/)

Instalar `surge` con el comando:

```bash
npm install -g surge
```

Una vez situado en la carpeta del proyecto:

```bash
npm run build
surge public nombre-app.surge.sh
```

## Manuel Alejandro Gallego - Camgrafiman
