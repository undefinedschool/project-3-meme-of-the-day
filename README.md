# Project 3: Meme Of The Day

Este es un proyecto para practicar e integrar lo visto sobre hacer _requests_ usando **[Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)**, **[Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)**, manipulación del **DOM**, **modularización**, **refactoring**, **Git** y **CSS**.

**Nota:** trabajar en un branch `dev` y pushear a `master`(haciendo PR) cuando tengamos una feature completa, siguiendo el [Feature Branch Workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow) como metodología.

## Parte 1: Request y procesamiento de los datos 🕵️‍♀️

0. Leer la [documentación](https://api.imgflip.com/) de la API de Memes
1. Crear un nuevo repo **(no fork!)** en GitHub para el código del ejercicio. Clonarlo para trabajar de forma local.
2. Dentro del repo, crear un archivo `index.js`, donde va a estar nuestro código.
3. Hacer un _request_ de tipo `GET` al endpoint `https://api.imgflip.com/get_memes`, usando `Fetch API`.
4. Investigar el objeto [Response](https://developer.mozilla.org/en-US/docs/Web/API/Response). Si la respuesta es exitosa (`status code: 200`), mostrar en consola el mensaje "Successful request!", sino mostrar "Oops, we got an error ${STATUS_CODE}", con el valor correspondiente. Ver [Handling Failed HTTP Responses With fetch()
](https://www.tjvantoll.com/2015/09/13/fetch-and-errors/)
5. A partir de la respuesta obtenida, generar el siguiente resultado:
    - Quedarnos sólo con las propiedades `id`, `name`, `width`, `height` y `url` (en ese orden) de cada elemento del array. Omitir el resto (**Tip:** usar [_destructuring_](https://github.com/undefinedschool/notes-es6-destructuring-notes)). Ver ejemplo más abajo.
    - Generar un nuevo array de _memes_, donde cada uno tendrá las propiedades mencionadas en el ítem anterior
    - En este array, filtraremos aquellos elementos cuyas propiedades `width` ó `height` tengan un valor < `500`
    - Ordenar el array por `id`, de forma ascendente
5. Mostrar el resultado en la consola. Recordá que podés usar `console.dir` para visualizar mejor objetos.
6. Usar siempre nombres declarativos para las variables, constantes, etc. [Guía de buenas prácticas](https://github.com/undefinedschool/best-practices).
7. En caso de error al hacer el request, mostrar el `message` del error.

```js
// resultado esperado
[
 {
   id: "93895088",
   name: "Expanding Brain",
   width: 857,
   height: 1202,
   url: "https://i.imgflip.com/1jwhww.jpg"
 },
 ...
]
```

## Parte 2: Modularización y refactoring 🛀

Vamos a separar el código en 2 archivos, `api.js` y `index.js`. Usar [ES6 Modules](https://github.com/undefinedschool/es6-modules/) para exportar e importar entre ambos.

- `api.js` va a contener el código necesario para realizar el _request_ a la API y retornar el array de memes _original_, sin modificaciones. 
  - este código irá dentro de la función `getMemes(URL)`, que recibe la _url_ como parámetro
  - guardar el endpoint de la API en una constante global `ENDPOINT`
- `index.js` va a importar la función `getMemes()` de `api.js`, invocarla y hacer todo el procesamiento posterior que hicimos en la [parte 1](#parte-1-request-y-procesamiento-de-los-datos)
  - modularizar los diferentes procesamientos que hacemos en los _callbacks_ en funciones y usarlas. Ver abajo cómo debería quedar

```
do1()
  .then(do2())
  .then(do3());
```

## Parte 3: Meme del día 📆

1. Escribir la función `getMemeOfTheDay()` (en `index.js`), que reciba un array de memes (resultado de la [parte 2](#parte-2-modularizar-y-refactorizar)) y retorne el meme correspondiente al día actual, es decir, si hoy fuera 21 de Octubre, debe retornar el meme Nº 21 de la lista, mañana el Nº 22, etc.
2. Analizar posibilidades de modularizar y refactorizar esta función y aplicarlas.

## Parte 4: Random! 🎰

1. Escribir la función `getRandomMeme()` (en `index.js`), que reciba un array de memes (resultado de la [parte 2](#parte-2-modularizar-y-refactorizar)) y retorne, de forma aleatoria, algún _meme_ del mismo.
2. Analizar posibilidades de modularizar y refactorizar esta función y aplicarlas.

## Parte 5: Render 👀

1. Crear un `index.html` en el mismo repo, usando la estructura predefinida de un HTML5 vacío.
2. Crear dentro un `div` con la clase `container`.
   - Usar [Flexbox](https://www.youtube.com/watch?v=JJSoEo8JSnc) para centrar (horizontal y verticalmente) todo el contenido de este `div`
   - Agregarle un `h1` con el texto "Meme of the Day"
   - Agregarle **debajo** un tag `img` con la clase `meme` y asignarle como `src` el meme obtenido con la función `getMemeOfTheDay()`
   - Agregar un botón **debajo** del `img`, con la clase `btn-get-random-meme` y el texto "Get random Meme!"

Abajo se muestra cómo quedaría la estructura

```
  container
    |-- h1
    |-- img
    |-- button
```

3. Al hacer click en el botón, debe ocurrir lo siguiente:
  - Modificar el texto del `h1` a "Random Meme"
  - Modificar el texto del botón a "Get another random Meme!"
  - Utilizar la función `getRandomMeme()` de la [parte 4](#parte-4-random) para obtener un meme aleatorio
    - Setear la `url` del meme random como `src` de la imagen obtenida
    - Setear el `name` del meme como random `alt` de la imagen obtenida

## Parte 6: Estilizando 💅

1. Crear el archivo `styles.css`, donde irá todo el código que usaremos para los estilos.
2. Aplicar el _reset_ con `padding: 0`, `margin: 0` y `box-sizing: border-box` donde corresponda.
3. Usar fuentes de [Google Fonts](https://fonts.google.com/) para los `h1`y `h2`.
4. Aplicar los estilos necesarios para que los elementos del container queden con la estructura y orden definidos en la [parte 5](#parte-5-render).
5. Aplicar márgenes entre los diferentes elementos del container.
6. Agregar [efectos y transiciones](https://dev.to/webdeasy/top-20-css-buttons-animations-f41) al botón, al hacerle _hover_ y clickearlo.
7. Al hacer _hover_ sobre la imagen del meme, se debe visualizar un texto con transición **sobre** la imagen, con el `name` del meme como texto. Ver [texto con transición _fade in_](https://www.w3schools.com/howto/howto_css_image_overlay.asp) como ejemplo. 
8. Agregar una transición al cambiar de imagen, cada vez que obtenemos un nuevo meme random. En [este ejemplo](http://jsfiddle.net/mhRec/2/) la imagen se traslada hacia la derecha, en nuestro caso será hacia la izquierda.
10. Agregar todos los estilos que consideren necesarios

## Parte 6 BIS: Viento de cola 🌬

Implementar los estilos del proyecto utilizando [Tailwind CSS](https://github.com/undefinedschool/notes-tailwind-css/)

## Parte 7: README 📝

Agregar un archivo *README* al proyecto, que incluya (al menos):

- descripción del proyecto
- stack (tecnologías) utilizadas
- pasos para correrlo localmente
- cualquier otro detalle técnico que consideren relevante (decisiones que hayan tomado, etc)

👉 Más información y recomendaciones sobre [cómo escribir un buen README](https://bulldogjob.com/news/449-how-to-write-a-good-readme-for-your-github-project)

## Parte 8: `header`, `footer` y _HTML semántico_ 🖋️

1. Agregar un `header` que tenga, a la derecha, un link al repositorio de GitHub con el código del proyecto. El link debe ser un ícono de GitHub, para lo que pueden usar [Font Awesome](https://fontawesome.com/). Ver ejemplo debajo

![](https://i.imgur.com/WMthd4P.png)

2. Agregar un `footer` que contenga info como el año, autor/a del proyecto y link al perfil de GitHub. Pueden agregar links adicionales si lo consideran, como LinkedIn, alguna red social, etc. Ver ejemplos debajo

#### Ejemplo 1

![](https://i.imgur.com/ysWEGS5.png)

#### Ejemplo 2

![](https://i.imgur.com/bfAwRND.png)

3. Agregar los tags _semánticos_ de HTML5 necesarios. Recuerden que siempre tiene que haber un `main`, puede o no haber `section`, etc

## Parte 9: Tests de accesibilidad y performance 😄

Uno de los mayores beneficios de escribir _HTML semántico_ es la mejora en la [accesibilidad](https://www.youtube.com/watch?v=gQIKQO41pME) de un sitio. Por esta razón es importante que tratemos siempre de utilizar las etiquetas correctas, con los atributos necesarios. También es importante testear nuestra aplicación simulando conexiones más lentas (la pestaña _Networking_ permite hacer esto, se llama [_throttling_](https://en.wikipedia.org/wiki/Bandwidth_throttling)), asegurarnos de que el contraste generado por los colores de texto y background son suficientes, etc.

Para esto vamos a utilizar algunas herramientas que van a ayudarnos a analizar estos detalles y obtener sugerencias.

1. Instalar la extensión axe ([Chrome](https://chrome.google.com/webstore/detail/axe-web-accessibility-tes/lhdoppojpmngadmnindnejefpokejbdd?hl=en-US), [Firefox](https://addons.mozilla.org/en-US/firefox/addon/axe-devtools/)), usarla para analizar la accesibilidad del sitio y aplicar en lo posible las sugerencias
2. Después de _hostear_ tu sitio en algunas de las opciones que vimos, poner la url en [web.dev](https://web.dev/measure/) y correr el test. Observar el reporte con los resultados obtenidos y analizar qué cambios se pueden aplicar

## Parte 10: async & defer

1. Usar [font-display](https://scotch.io/bar-talk/google-fonts-now-supports-font-display) para cargar las Google Fonts, agregando `&display=fallback` a las urls
2. Mover el `<script>` con el `index.js` del HTML al final del tag `head` y usar el atributo [`defer`](https://flaviocopes.com/javascript-async-defer/) para que el script que linkeamos en el HTML cargue de forma asincrónica:

`<script defer src="index.js" type="module"></script>`

## Parte 11: Hosting 🚀

- Ver notas de [deployment](https://github.com/undefinedschool/notes-deployment/)

Investigar cómo y hostear el proyecto usando 
  - [GitHub Pages](https://pages.github.com/)
  - [Now](https://zeit.co/github)
  - [Netlify](https://www.netlify.com/)
  
