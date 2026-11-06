# Guía de Referencia: HTML5 y CSS3 (Módulo: Lenguajes de Marcas)

Esta guía recopila los conceptos fundamentales de HTML y CSS necesarios para el ciclo de **Desarrollo de Aplicaciones Multiplataforma (DAM)**.

---

## 1. Etiquetas Básicas de HTML

HTML (*HyperText Markup Language*) es el lenguaje estándar utilizado para estructurar el contenido de las páginas web.

### Estructura Mínima de un Documento

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">s
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mi Primera Página</title>
</head>
<body>
    <h1>¡Hola, Mundo!</h1>
    <p>Este es el contenido principal.</p>
</body>
</html>
```

* `<!DOCTYPE html>` indica que se utiliza HTML5 y debe aparecer en la primera línea.
* `<html lang="es">` es el elemento raíz; `lang` informa del idioma a buscadores y lectores de pantalla.
* `<head>` contiene metadatos y recursos que no forman parte del contenido visible.
* `charset="UTF-8"` permite representar correctamente tildes, eñes y otros caracteres.
* La etiqueta `viewport` adapta el ancho a móviles y tabletas.
* `<title>` define el texto de la pestaña del navegador.
* `<body>` contiene todo el contenido visible.

### Elementos, atributos y anidamiento

Un elemento suele tener una etiqueta de apertura, contenido y una de cierre:

```html
<p class="aviso">Mañana hay examen.</p>
```

`class="aviso"` es un **atributo**: añade información al elemento y se escribe en la etiqueta de apertura. Algunos elementos, como `<img>`, `<input>`, `<meta>` y `<link>`, no admiten contenido interno ni utilizan etiqueta de cierre. Por ejemplo, se escribe `<img src="foto.jpg" alt="Descripción">`, sin añadir `</img>`.

Los elementos anidados deben cerrarse en orden inverso al que se abren:

```html
<!-- Correcto -->
<p>Estamos aprendiendo <strong>HTML</strong>.</p>

<!-- Incorrecto: las etiquetas se cruzan -->
<p>Estamos aprendiendo <strong>HTML.</p></strong>
```

La sangría no modifica el resultado, pero muestra las relaciones padre-hijo y ayuda a localizar errores.

### Etiquetas Principales de Texto y Enlaces

| Etiqueta | Descripción | Ejemplo |
| :--- | :--- | :--- |
| `<h1>` a `<h6>` | Encabezados jerárquicos (`h1` es el más importante). | `<h1>Título Principal</h1>` |
| `<p>` | Párrafo de texto. | `<p>Texto explicativo...</p>` |
| `<a>` | Enlace (*hyperlink*). Usa el atributo `href`. | `<a href="https://google.com">Buscar</a>` |
| `<img>` | Inserta una imagen. No utiliza etiqueta de cierre y requiere `src` y `alt`. | `<img src="logo.png" alt="Logo de la empresa">` |
| `<span>` | Contenedor en línea (*inline*) para dar estilo o manipular texto. | `<span class="destacado">texto</span>` |
| `<div>` | Contenedor en bloque (*block*) para agrupar elementos. | `<div>...</div>` |

Los encabezados expresan jerarquía, no un tamaño visual. Lo normal es un `<h1>` que identifica el tema principal, seguido de `<h2>` para apartados y `<h3>` para subapartados. Su aspecto se modifica con CSS.

`<strong>` señala contenido importante y `<em>` aporta énfasis. Para mostrar código se utiliza `<code>`; si debe conservar espacios y saltos de línea, se combina con `<pre>`.

### Enlaces, imágenes y rutas

`href` indica el destino de un enlace. Puede ser una URL externa, otro archivo o una sección identificada mediante `id`:

```html
<a href="https://developer.mozilla.org/es/">Documentación de MDN</a>
<a href="paginas/contacto.html">Contacto</a>
<a href="#listas">Ir al apartado de listas</a>

<h3 id="listas">Listas</h3>
```

Una ruta relativa se calcula desde el archivo HTML actual. `imagenes/logo.png` entra en una carpeta y `../index.html` sube una carpeta. Este es uno de los motivos más frecuentes por los que una imagen o un enlace no funciona.

El atributo `alt` describe la información de una imagen para quien no pueda verla. Si es decorativa se escribe `alt=""`; no se debe omitir.

```html
<img src="imagenes/aula.jpg"
     alt="Alumnado trabajando con ordenadores en el aula"
     width="800" height="450">
```

### Listas

#### Listas no ordenadas (`<ul>`)
```html
<ul>
    <li>Java</li>
    <li>HTML/CSS</li>
    <li>SQL</li>
</ul>
```

#### Listas ordenadas (`<ol>`)
```html
<ol>
    <li>Descargar repositorio</li>
    <li>Compilar código</li>
    <li>Ejecutar aplicación</li>
</ol>
```

### Tablas de datos

Las tablas representan datos relacionados en filas y columnas. No deben utilizarse para colocar elementos o diseñar la página; para eso existen Flexbox y Grid.

```html
<table>
    <caption>Calificaciones de la primera evaluación</caption>
    <thead>
        <tr>
            <th scope="col">Alumno</th>
            <th scope="col">HTML</th>
            <th scope="col">CSS</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="row">Alicia</th>
            <td>8</td>
            <td>7</td>
        </tr>
        <tr>
            <th scope="row">Hugo</th>
            <td>6</td>
            <td>9</td>
        </tr>
    </tbody>
</table>
```

* `<caption>` proporciona un título que explica la tabla.
* `<thead>` y `<tbody>` separan la cabecera de los datos.
* `<tr>` crea una fila, `<th>` una celda de encabezado y `<td>` una celda de datos.
* `scope="col"` y `scope="row"` relacionan los encabezados con sus datos y mejoran la accesibilidad.

---

## 2. HTML Semántico

La **semántica** es el significado. El HTML semántico consiste en elegir etiquetas que indiquen qué función cumple el contenido, en lugar de usar contenedores genéricos para todo.

Un `<div>` solamente indica que existe un bloque. En cambio, `<nav>` indica que el bloque contiene navegación, `<article>` que es una pieza independiente y `<footer>` que contiene información final. Dos páginas pueden tener el mismo aspecto visual y, sin embargo, una estar mucho mejor estructurada que la otra.

```html
<!-- Estructura poco descriptiva -->
<div class="cabecera">...</div>
<div class="menu">...</div>
<div class="contenido">...</div>

<!-- Estructura semántica -->
<header>...</header>
<nav>...</nav>
<main>...</main>
```

### 2.1. ¿Por qué es importante?

* **Accesibilidad:** los lectores de pantalla pueden localizar la navegación, el contenido principal y las distintas regiones.
* **Mantenimiento:** otro desarrollador entiende más rápido la organización del documento.
* **Buscadores:** pueden interpretar mejor el tema y la importancia de cada contenido.
* **Consistencia:** obliga a pensar en la jerarquía antes de aplicar estilos.

La etiqueta no determina la posición. `<aside>` no significa «caja situada a la derecha» y `<nav>` no crea automáticamente un menú horizontal. **HTML define el significado; CSS define la presentación.**

### 2.2. Etiquetas estructurales principales

#### `<header>`: cabecera

Contiene información introductoria: título, logotipo, descripción, buscador o navegación. Puede haber una cabecera general y otras dentro de un `<article>` o una `<section>`.

```html
<header>
    <img src="logo.svg" alt="Aula DAM">
    <h1>Portal de 1.º DAM</h1>
    <p>Recursos y actividades del curso</p>
</header>
```

No debe confundirse con `<head>`: este último contiene metadatos no visibles, mientras que `<header>` forma parte del contenido visible.

#### `<nav>`: navegación

Agrupa enlaces importantes, como el menú principal, un índice del tema o una paginación. No es necesario envolver en `<nav>` cualquier pareja de enlaces.

```html
<nav aria-label="Navegación principal">
    <ul>
        <li><a href="index.html">Inicio</a></li>
        <li><a href="modulos.html">Módulos</a></li>
        <li><a href="contacto.html">Contacto</a></li>
    </ul>
</nav>
```

`aria-label` permite distinguir esta navegación si hay varias. Los enlaces se colocan en una lista porque forman un conjunto relacionado.

#### `<main>`: contenido principal

Contiene la información principal y exclusiva de la página. Debe existir como máximo un `<main>` visible por documento. No incluye el menú general ni el pie que se repiten en todas las páginas.

#### `<section>`: sección temática

Agrupa una parte reconocible de un documento. Normalmente debe tener un encabezado que indique su tema.

```html
<section>
    <h2>Resultados de aprendizaje</h2>
    <p>Al finalizar la unidad, el alumnado podrá...</p>
</section>
```

No se usa `<section>` solo para crear una caja o aplicar CSS. Si el bloque no tiene tema propio y únicamente sirve para agrupar elementos, suele ser más apropiado `<div>`.

#### `<article>`: contenido independiente

Representa una pieza que podría entenderse o distribuirse por separado: una noticia, entrada de blog, ficha de producto, mensaje de un foro o comentario.

```html
<article>
    <header>
        <h2>Cómo validar un documento HTML</h2>
        <p>Publicado el <time datetime="2026-10-30">30 de octubre</time></p>
    </header>
    <p>La validación permite detectar errores de sintaxis...</p>
    <footer><p>Autor: Ana Pérez</p></footer>
</article>
```

Un artículo puede contener secciones y una sección puede reunir varios artículos. Para elegir:

* Si el contenido tiene sentido por sí solo, probablemente es un `<article>`.
* Si es una parte temática de un contenido mayor, probablemente es una `<section>`.
* Si solo se necesita un contenedor para diseño, se utiliza `<div>`.

#### `<aside>`: contenido complementario

Contiene información relacionada de manera secundaria: un glosario, enlaces relacionados, una biografía o una advertencia. Significa «complementario», no «colocado a un lado»; en un móvil puede aparecer debajo.

```html
<aside>
    <h2>Recuerda</h2>
    <p>Las etiquetas semánticas describen la función del contenido.</p>
</aside>
```

#### `<footer>`: pie

Incluye información final sobre una página, sección o artículo: autoría, licencia, copyright, datos de contacto o enlaces legales. Puede haber varios pies en el mismo documento.

### 2.3. Otros elementos semánticos útiles

`<time>` representa una fecha u hora. `datetime` la expresa en un formato que las máquinas pueden interpretar:

```html
<time datetime="2026-11-06T10:15">6 de noviembre a las 10:15</time>
```

`<figure>` agrupa una imagen, esquema o fragmento que puede llevar un pie:

```html
<figure>
    <img src="modelo-caja.png" alt="Diagrama del modelo de caja CSS">
    <figcaption>Contenido, relleno, borde y margen.</figcaption>
</figure>
```

`<details>` crea información desplegable y `<summary>` su título:

```html
<details>
    <summary>Ver solución</summary>
    <p>La etiqueta adecuada es &lt;article&gt;.</p>
</details>
```

### 2.4. Ejemplo completo

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Blog Dev</title>
</head>
<body>

    <!-- Encabezado superior de la web -->
    <header>
        <h1>DevBlog DAM</h1>
        <nav>
            <ul>
                <li><a href="#inicio">Inicio</a></li>
                <li><a href="#articulos">Artículos</a></li>
            </ul>
        </nav>
    </header>

    <!-- Contenido principal exclusivo del documento -->
    <main>
        <section id="articulos">
            <article>
                <h2>Introducción a Lenguajes de Marcas</h2>
                <p>Publicado el <time datetime="2026-10-29">29 de Octubre</time></p>
                <p>Las marcas permiten estructurar información...</p>
            </article>
        </section>

        <!-- Contenido complementario -->
        <aside>
            <h3>Enlaces de interés</h3>
            <p>Documentación oficial de MDN.</p>
        </aside>
    </main>

    <!-- Pie de página -->
    <footer>
        <p>&copy; 2026 - Módulo Lenguajes de Marcas (1º DAM)</p>
    </footer>

</body>
</html>
```

La estructura se entiende incluso sin ver sus estilos: existe una cabecera con navegación, un contenido principal, una sección que contiene un artículo, información complementaria y un pie. Esa capacidad de explicar el documento es la finalidad del HTML semántico.

### 2.5. Semántica y accesibilidad

* Mantener una jerarquía lógica de encabezados; no elegirlos por su tamaño visual.
* Asociar cada campo de formulario con un `<label>`.
* Escribir un `alt` útil en imágenes informativas y `alt=""` en las decorativas.
* Usar `<button>` para ejecutar acciones y `<a>` para navegar a otro recurso.
* Incluir `lang` en `<html>` y un `<title>` descriptivo.
* Usar primero el elemento HTML nativo adecuado. Por ejemplo, `<button>` es preferible a `<div role="button">`.

---

## 3. Formularios en HTML

Los formularios permiten a los usuarios enviar información desde el cliente hacia el servidor (clave para el desarrollo backend).

### Contenedor Principal: `<form>`

* **`action`**: URL o endpoint a donde se enviarán los datos.
* **`method`**: Método HTTP (`GET` para consultas, `POST` para enviar datos sensibles o crear registros).

### Elementos Básicos de un Formulario

```html
<form action="/registro" method="POST">
    
    <!-- Campo de Texto -->
    <div>
        <label for="nombre">Nombre completo:</label>
        <input type="text" id="nombre" name="nombre" placeholder="Ej: Ana Gómez" required>
    </div>

    <!-- Campo de Correo Electrónico -->
    <div>
        <label for="email">Correo electrónico:</label>
        <input type="email" id="email" name="email" required>
    </div>

    <!-- Campo de Contraseña -->
    <div>
        <label for="password">Contraseña:</label>
        <input type="password" id="password" name="password" minlength="8" required>
    </div>

    <!-- Menú Desplegable (<select>) -->
    <div>
        <label for="curso">Curso escolar:</label>
        <select id="curso" name="curso">
            <option value="dam1">1º DAM</option>
            <option value="dam2">2º DAM</option>
            <option value="daw1">1º DAW</option>
        </select>
    </div>

    <!-- Área de Texto Multilínea -->
    <div>
        <label for="comentario">Comentarios:</label>
        <textarea id="comentario" name="comentario" rows="4"></textarea>
    </div>

    <!-- Botón de Envío -->
    <button type="submit">Guardar Registro</button>

</form>
```

> **Nota clave para Backend:** El atributo `name` en los `<input>` es el nombre de la clave que recibirá la petición HTTP en el servidor (ej: `request.getParameter("nombre")`).

### Relación entre `label`, `id`, `name` y `value`

```html
<label for="usuario">Usuario:</label>
<input type="text" id="usuario" name="usuario" value="ana">
```

* `for="usuario"` conecta la etiqueta con el control cuyo `id` coincide.
* `id` identifica al elemento dentro del documento y debe ser único.
* `name` es la clave que recibirá el servidor. Sin `name`, el dato no se envía.
* `value` es el valor inicial y, en ciertos controles, el valor enviado.

`GET` añade los datos a la URL y es adecuado para búsquedas o filtros que no modifican información. `POST` los envía en el cuerpo de la petición y se usa al crear o modificar datos. **POST no cifra la información**: la protección durante el envío depende de HTTPS.

### Selección de opciones

Los botones `radio` que comparten el mismo `name` forman un grupo de selección única:

```html
<fieldset>
    <legend>Turno preferido</legend>
    <input type="radio" id="manana" name="turno" value="manana" checked>
    <label for="manana">Mañana</label>

    <input type="radio" id="tarde" name="turno" value="tarde">
    <label for="tarde">Tarde</label>
</fieldset>
```

Las casillas `checkbox` permiten decisiones independientes. `<fieldset>` agrupa controles relacionados y `<legend>` da nombre al grupo.

```html
<input type="checkbox" id="condiciones" name="acepta_condiciones" required>
<label for="condiciones">Acepto las condiciones</label>
```

### Validación HTML

```html
<input type="text" name="usuario" required minlength="4" maxlength="20">
<input type="number" name="edad" min="16" max="99">
<input type="email" name="correo" autocomplete="email" required>
```

* `required` hace obligatorio el control.
* `min`, `max`, `minlength` y `maxlength` establecen límites.
* `pattern` permite exigir un patrón mediante una expresión regular.
* `placeholder` ofrece una pista, pero **no sustituye a `<label>`**.
* `readonly` impide editar el campo, pero su valor se envía.
* `disabled` desactiva el campo y su valor no se envía.

La validación del navegador mejora la experiencia, pero el servidor siempre debe validar de nuevo: un cliente puede manipular o enviar directamente cualquier petición.

---

## 4. CSS básico

CSS (*Cascading Style Sheets*) se encarga del estilo visual de los documentos HTML.

Esta primera parte contiene lo imprescindible para aplicar una presentación sencilla a una página: conectar la hoja de estilos, escribir reglas, seleccionar elementos y controlar sus espacios y bordes. Se puede estudiar como un bloque independiente antes de comenzar JavaScript.

### 4.1. Vinculación recomendada (Hoja de Estilos Externa)

En la sección `<head>` de tu documento HTML, añade:

```html
<link rel="stylesheet" href="estilos.css">
```

### 4.2. Sintaxis de una Regla CSS

```css
selector {
    propiedad: valor;
    propiedad2: valor2;
}
```

### 4.3. Selectores Básicos

1. **Selector de Etiqueta**: Afecta a todos los elementos del mismo tipo.
   ```css
   h1 {
       color: #1a365d;
       font-family: Arial, sans-serif;
   }
   ```

2. **Selector de Clase (`.`)**: Reutilizable en múltiples elementos.
   ```css
   .campo-formulario {
       border: 1px solid #cbd5e0;
       border-radius: 4px;
   }
   ```

3. **Selector de ID (`#`)**: Único por elemento en la página.
   ```css
   #boton-login {
       background-color: #2b6cb0;
       color: white;
   }
   ```

### 4.4. Propiedades básicas de presentación

Las siguientes propiedades permiten cambiar el aspecto general de textos y cajas sin modificar la estructura HTML.

#### Colores y fondos

```css
body {
    color: #333333;
    background-color: #f0f4f8;
}
```

* `color` establece el color del texto.
* `background-color` establece el color de fondo.

Los colores pueden escribirse mediante nombres, como `white`, o mediante códigos hexadecimales, como `#2b6cb0`. En un código hexadecimal, cada pareja representa la cantidad de rojo, verde y azul.

#### Tipografía y alineación

```css
body {
    font-family: Arial, sans-serif;
    font-size: 16px;
}

h1 {
    text-align: center;
}

label {
    font-weight: bold;
}
```

* `font-family` establece el tipo de letra. Si Arial no está disponible, se utiliza cualquier fuente de la familia `sans-serif`.
* `font-size` establece el tamaño del texto.
* `font-weight` controla su grosor; por ejemplo, `bold` muestra negrita.
* `text-align` alinea el contenido en horizontal: `left`, `center` o `right`.

#### Anchura y centrado

```css
main {
    width: 80%;
    margin: 30px auto;
}
```

`width` establece la anchura. En este ejemplo, `<main>` ocupa el 80 % del espacio disponible. En `margin: 30px auto`, los `30px` se aplican arriba y abajo, mientras que `auto` reparte el espacio de izquierda y derecha y centra la caja.

#### Valores abreviados de `margin` y `padding`

`margin` y `padding` permiten indicar varios lados en una sola declaración:

```css
.ejemplo {
    padding: 10px;             /* Los cuatro lados */
    margin: 10px 20px;         /* Vertical | horizontal */
    padding: 5px 10px 15px;    /* Arriba | horizontal | abajo */
    margin: 5px 10px 15px 20px; /* Arriba | derecha | abajo | izquierda */
}
```

Cuando se escriben cuatro valores, puede recordarse el orden siguiendo las agujas del reloj: arriba, derecha, abajo e izquierda.

#### Cursor del ratón

```css
button {
    cursor: pointer;
}
```

`cursor: pointer` muestra el cursor con forma de mano y ayuda a reconocer que el elemento se puede pulsar.

### 4.5. Primer estado interactivo: `:hover`

Una **pseudoclase** selecciona un elemento cuando se encuentra en un estado determinado. `:hover` se aplica mientras el puntero está situado sobre él:

```css
#btn-enviar {
    color: white;
    background-color: #2f855a;
}

#btn-enviar:hover {
    background-color: #276749;
}
```

El botón conserva normalmente el primer color y se oscurece al colocar el puntero encima. `:hover` debe utilizarse como una ayuda visual, no como la única forma de mostrar información importante.

### 4.6. El Modelo de Caja (*Box Model*)

Cada elemento HTML renderizado es una caja rectangular compuesta por 4 áreas:

* **Content**: El contenido real (texto, imagen, inputs).
* **Padding**: Espacio **interior** entre el contenido y el borde.
* **Border**: El borde visible que rodea el padding.
* **Margin**: Espacio **exterior** entre la caja y los demás elementos colindantes.

El siguiente esquema representa las capas desde el exterior hacia el interior:

```text
┌──────────────────────────────────────────────────────┐
│                        MARGIN                        │
│                                                      │
│    ┌────────────────────────────────────────────┐    │
│    │                   BORDER                   │    │
│    │                                            │    │
│    │    ┌──────────────────────────────────┐    │    │
│    │    │             PADDING              │    │    │
│    │    │                                  │    │    │
│    │    │    ┌────────────────────────┐    │    │    │
│    │    │    │        CONTENT         │    │    │    │
│    │    │    │ Texto, imagen, input…  │    │    │    │
│    │    │    └────────────────────────┘    │    │    │
│    │    │                                  │    │    │
│    │    └──────────────────────────────────┘    │    │
│    │                                            │    │
│    └────────────────────────────────────────────┘    │
│                                                      │
└──────────────────────────────────────────────────────┘
```

En español, estas capas corresponden a **margen**, **borde**, **relleno** y **contenido**. El margen queda fuera del borde; el relleno queda dentro del borde y rodea al contenido.

```css
.tarjeta {
    width: 300px;           /* Ancho del contenido */
    padding: 16px;          /* Espacio interno */
    border: 2px solid #ccc; /* Borde visible */
    margin: 20px;           /* Separación externa */
}
```

Con el valor predeterminado `box-sizing: content-box`, el ancho declarado solo corresponde al contenido: el relleno y el borde se suman. Para que el ancho incluya las tres partes suele aplicarse:

```css
*,
*::before,
*::after {
    box-sizing: border-box;
}
```

---

## 5. CSS intermedio

Esta segunda parte amplía los fundamentos. Explica cómo resolver conflictos entre reglas, seleccionar elementos con más precisión y construir diseños adaptables con Flexbox y Grid. Puede abordarse después o utilizarse como material de consulta durante proyectos más completos.

### 5.1. Selectores combinados y otros estados

```css
nav a { text-decoration: none; }       /* a dentro de nav */
ul > li { margin-bottom: 0.5rem; }     /* li hijo directo de ul */
h2 + p { font-size: 1.1rem; }          /* p inmediatamente posterior */
input[required] { border-left: 4px solid red; }
a:focus-visible { outline: 3px solid orange; }
```

Después de conocer `:hover`, se pueden utilizar otras pseudoclases. `:focus-visible` representa el foco de teclado y permite mostrar con claridad qué enlace o control está seleccionado. Las pantallas táctiles no siempre disponen de `:hover`, por lo que no se debe depender únicamente de ese estado.

### 5.2. Cascada, especificidad y herencia

Varias reglas pueden afectar al mismo elemento. El navegador resuelve el conflicto mediante la **cascada**: tiene en cuenta el origen, la importancia, la especificidad y, si hay empate, el orden de aparición.

```css
p { color: black; }          /* Selector de etiqueta */
.destacado { color: blue; }  /* Selector de clase */
#resumen { color: green; }   /* Selector de id */
```

En `<p id="resumen" class="destacado">`, el texto será verde. De forma simplificada, un `id` es más específico que una clase y una clase más que una etiqueta. Conviene usar selectores sencillos y evitar `!important`, porque dificulta modificar los estilos más adelante.

Propiedades como `color` y `font-family` suelen heredarse de padres a hijos; `margin`, `padding` y `border` no:

```css
body {
    color: #222;
    font-family: Arial, sans-serif;
    line-height: 1.6;
}
```

### 5.3. Unidades y tamaños

* `px`: píxeles CSS, útiles para bordes y detalles concretos.
* `%`: porcentaje relativo al contexto.
* `rem`: relativo al tamaño de letra del elemento raíz; útil para textos y espacios coherentes.
* `em`: relativo al tamaño de letra del elemento o su padre, según la propiedad.
* `vw` y `vh`: porcentaje del ancho y alto de la ventana.

```css
main {
    width: 92%;
    max-width: 70rem;
    margin-inline: auto;
}
```

Combinar `width` y `max-width` hace que el contenido aproveche pantallas pequeñas sin resultar demasiado ancho en las grandes.

### 5.4. Flujo normal y propiedad `display`

Los elementos de bloque, como `<p>`, `<div>` y `<section>`, comienzan normalmente en una línea nueva. Los elementos en línea, como `<a>`, `<span>` y `<strong>`, ocupan solo el espacio de su contenido.

CSS puede cambiar su presentación sin cambiar su significado:

```css
a.boton { display: inline-block; }
.oculto { display: none; }
```

`display: none` elimina el elemento de la presentación y también de la lectura de tecnologías de asistencia.

### 5.5. Maquetación con Flexbox

Flexbox distribuye elementos principalmente en una fila o una columna. `display: flex` se aplica al **contenedor padre**:

```css
.menu {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    gap: 1rem;
}
```

* `flex-direction` establece el eje principal.
* `justify-content` reparte espacio en ese eje.
* `align-items` alinea en el eje transversal.
* `gap` separa elementos sin añadir márgenes individuales.
* `flex-wrap` permite crear otra línea cuando falta espacio.

### 5.6. Maquetación con Grid

Grid organiza elementos en filas y columnas:

```css
.rejilla {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(16rem, 1fr));
    gap: 1rem;
}
```

`1fr` significa una fracción del espacio disponible. En este ejemplo, cada columna mide al menos `16rem`; se crean tantas como quepan y pasan a nuevas filas cuando disminuye el ancho.

Grid suele resultar útil para la estructura o las rejillas de tarjetas; Flexbox, para alinear componentes en una dirección. Se pueden combinar.

### 5.7. Diseño adaptable

Las *media queries* aplican reglas cuando se cumple una condición. Es recomendable comenzar con el diseño para pantallas pequeñas y ampliarlo cuando exista espacio:

```css
.contenido {
    display: grid;
    gap: 1rem;
}

@media (min-width: 48rem) {
    .contenido {
        grid-template-columns: 2fr 1fr;
    }
}

img {
    max-width: 100%;
    height: auto;
}
```

Los puntos de ruptura deben elegirse cuando el contenido deja de verse bien, no para un modelo concreto de móvil.

---

## 6. Ejemplo completo integrado

### HTML (`index.html`)

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Acceso al Sistema</title>
    <link rel="stylesheet" href="estilos.css">
</head>
<body>

    <main class="contenedor">
        <form action="/login" method="POST" class="form-login">
            <h1>Iniciar Sesión</h1>

            <div class="grupo-campo">
                <label for="usuario">Usuario:</label>
                <input type="text" id="usuario" name="usuario" class="campo" required>
            </div>

            <div class="grupo-campo">
                <label for="clave">Contraseña:</label>
                <input type="password" id="clave" name="clave" class="campo" required>
            </div>

            <button type="submit" id="btn-entrar">Acceder</button>
        </form>
    </main>

</body>
</html>
```

### CSS (`estilos.css`)

```css
/* El ancho declarado incluye padding y border */
*,
*::before,
*::after {
    box-sizing: border-box;
}

/* Reset básico de márgenes */
body {
    margin: 0;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background-color: #f7fafc;
}

/* Centrado del contenedor */
.contenedor {
    width: min(350px, 92%);
    margin: 50px auto;
}

/* Estilo de la tarjeta de formulario */
.form-login {
    background-color: #ffffff;
    padding: 24px;
    border: 1px solid #e2e8f0;
    border-radius: 8px;
}

.form-login h1 {
    margin-top: 0;
    color: #2d3748;
    text-align: center;
}

/* Agrupación de campos */
.grupo-campo {
    margin-bottom: 16px;
}

.grupo-campo label {
    display: block;
    margin-bottom: 6px;
    color: #4a5568;
    font-weight: 600;
}

.campo {
    width: 100%;
    padding: 8px;
    border: 1px solid #cbd5e0;
    border-radius: 4px;
}

/* Botón principal */
#btn-entrar {
    width: 100%;
    padding: 10px;
    background-color: #3182ce;
    color: #ffffff;
    border: none;
    border-radius: 4px;
    font-size: 16px;
    cursor: pointer;
}

#btn-entrar:hover {
    background-color: #2b6cb0;
}

#btn-entrar:focus-visible,
.campo:focus-visible {
    outline: 3px solid #ed8936;
    outline-offset: 2px;
}
```

---

## 7. Errores habituales y lista de comprobación

### Errores frecuentes en HTML

* Repetir un mismo `id` en varios elementos.
* Usar encabezados por su tamaño en vez de por su jerarquía.
* Escribir varios `<br>` para crear espacio en lugar de usar CSS.
* Omitir `alt` en imágenes o `<label>` en formularios.
* Usar una tabla para maquetar la página.
* Emplear `<section>` como sustituto automático de cualquier `<div>`.
* Crear una acción con `<a>` sin destino o una navegación con un `<button>`.
* Escribir mal una ruta relativa o confundir mayúsculas y minúsculas.

### Errores frecuentes en CSS

* Olvidar `.` delante de una clase o `#` delante de un identificador.
* Usar `=` en vez de `:` entre propiedad y valor.
* Omitir unidades: `margin: 10` no es válido; `margin: 10px` sí.
* Confundir `margin` (espacio exterior) y `padding` (espacio interior).
* Aplicar Flexbox o Grid a los hijos en lugar de al contenedor.
* Depender de `!important` o crear selectores innecesariamente específicos.
* Fijar anchos que producen desplazamiento horizontal en móviles.

### Antes de entregar una página

1. Comprobar que el HTML describe correctamente el significado del contenido.
2. Revisar la jerarquía de encabezados como si fuera el índice de un tema.
3. Probar enlaces, imágenes y conexión con la hoja CSS.
4. Navegar solamente con teclado usando `Tab`, `Mayús + Tab` y `Enter`.
5. Probar varios anchos con las herramientas de desarrollo del navegador.
6. Usar el inspector para saber qué reglas CSS se aplican o quedan sobrescritas.
7. Validar HTML y CSS para detectar errores de sintaxis.

> **Idea para recordar:** HTML describe qué es el contenido; CSS decide cómo se presenta. Primero se construye una estructura válida, semántica y accesible; después se diseña.

---

## 8. Validación de HTML y CSS

Validar consiste en comprobar que el código respeta las reglas de sintaxis del lenguaje. Una página puede parecer correcta en el navegador y contener errores, porque los navegadores intentan interpretar y corregir automáticamente el código defectuoso.

La validación ayuda a:

* Detectar etiquetas mal cerradas o colocadas en un lugar incorrecto.
* Localizar atributos desconocidos, repetidos o con valores no válidos.
* Encontrar propiedades CSS mal escritas.
* Mejorar la compatibilidad entre navegadores.
* Mantener un código más claro y fácil de corregir.

### 8.1. Validar un documento HTML

Se puede utilizar el [validador de HTML del W3C](https://validator.w3.org/).

El validador ofrece distintas formas de introducir el documento:

1. **Validate by URI:** comprobar una página que ya está publicada en Internet.
2. **Validate by File Upload:** subir un archivo `.html` desde el equipo.
3. **Validate by Direct Input:** pegar directamente el código HTML.

Para una actividad realizada en local, la opción más sencilla es subir el archivo:

1. Abrir el validador.
2. Seleccionar **Validate by File Upload**.
3. Elegir, por ejemplo, `contacto.html`.
4. Pulsar **Check**.
5. Leer los mensajes, corregir el archivo y volver a validarlo.

Errores HTML frecuentes:

```html
<!-- Etiquetas cerradas en un orden incorrecto -->
<p>Texto <strong>importante</p></strong>

<!-- Dos elementos con el mismo identificador -->
<input id="correo">
<input id="correo">

<!-- Atributo obligatorio ausente -->
<img src="logo.png">
```

Las versiones corregidas serían:

```html
<p>Texto <strong>importante</strong></p>

<input id="correo-personal">
<input id="correo-empresa">

<img src="logo.png" alt="Logotipo de la empresa">
```

### 8.2. Validar una hoja de estilos

Para CSS se puede utilizar el [validador de CSS del W3C](https://jigsaw.w3.org/css-validator/).

También permite proporcionar una URL, subir un archivo `.css` o pegar el código. Para validar una hoja externa:

1. Abrir el validador de CSS.
2. Seleccionar la opción para subir un archivo.
3. Elegir `estilos.css`.
4. Iniciar la comprobación.
5. Corregir los errores indicados y repetir la validación.

Errores CSS frecuentes:

```css
/* Falta la unidad */
p {
    margin: 10;
}

/* Se ha escrito = en lugar de : */
h1 {
    color = blue;
}

/* Nombre de propiedad incorrecto */
body {
    background-colour: white;
}
```

Las versiones corregidas serían:

```css
p {
    margin: 10px;
}

h1 {
    color: blue;
}

body {
    background-color: white;
}
```

### 8.3. Errores y advertencias

El resultado puede mostrar dos tipos principales de mensajes:

* **Error:** indica que alguna parte del código no cumple las reglas del lenguaje y debe corregirse.
* **Advertencia (*warning*):** señala una situación que conviene revisar, aunque no siempre impide que el documento sea válido.

Los mensajes suelen indicar una línea aproximada, pero el problema puede haberse originado antes. Por ejemplo, una etiqueta que no se ha cerrado puede provocar varios mensajes posteriores.

### 8.4. Proceso recomendado

La validación no se realiza solamente al terminar. Es más fácil validar después de cada cambio importante:

1. Escribir una parte pequeña del documento.
2. Guardar y comprobar el resultado en el navegador.
3. Validar el HTML.
4. Validar la hoja CSS.
5. Corregir primero el error inicial y volver a comprobar.
6. Repetir hasta que no queden errores.
7. Probar la página en distintos tamaños de pantalla y, si es posible, en más de un navegador.

> Que un documento sea válido no garantiza que tenga un buen diseño o sea totalmente accesible, pero sí confirma que utiliza una sintaxis correcta y proporciona una base más fiable para continuar trabajando.
