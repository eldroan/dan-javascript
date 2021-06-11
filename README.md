# Javascript

> El siguiente texto es una guia teorica-pracitca sobre javascript escrita para la materia de desarrollo de aplicaciones en la nube de la carrera de ingeniería en sistemas de información - UTN FRSF

## Intro

Javascript es un lenguaje de programación que ejecuta en todos los browsers.

Por ejemplo, en Chrome podemos utilizar las herramientas de desarrolador para abrir una consola presionando Option + ⌘ + J (macOS), o Shift + CTRL + J (Windows/Linux)

![imagen de la consola de chrome](imagenes/01-console.png)

Dentro la consola de Chrome ingresamos expresiones de js como nuestro input `>` que luego se ejecutan y su resultado se imprime como output `<` en la terminal misma.

> TIP: La consola de Chrome es util para realizar pruebas mientras estamos aprendiendo ya que nos permite ver resultados inmediatos y sus herramientas de autocompletado e inspeccion son potentes.

Para poder escribir nuestro código y luego poder ejecutarlo vamos a necesitar un poco de ayuda de NodeJS, un entorno de ejecución de javascript, el cual está basado en el motor que utiliza Chrome.

Utilizando Node es que podemos ejecutar javascript en todos lados, incluso en servidores.

Para instalar node basta con dirigirnos a [https://nodejs.org/es/](https://nodejs.org/es/) para descargar e instalar la ultima version `LTS`. Otra alternativa es utilizar `nvm` (node version manager), para cuando necesitamos administrar multiples versiones, el cual se encuentra disponible para [linux/mac](https://github.com/nvm-sh/nvm#install--update-script) y [windows](https://github.com/coreybutler/nvm-windows#installation--upgrades)

Para comprobar si se instalo correctamente abrimos alguna terminal y ejecutamos

```bash
$ node -v
```

Deberiamos ver una respuesta indicando el numero de version de node indicandonos que todo salio bien

![terminal mostrando la versión de node](imagenes/02-node.png)

Con node instalado solo nos falta un editor de texto, vscode es una buena opción pero tambien existen otros.
Ahora solo nos falta abrir nuestro editor de texto de preferencia y estamos listo para empezar a escribir javascript.

## 0 - Hola mundo

Creando un archivo de extensión `.js` podemos empezar a escribir código, lo que escribamos aquí se ejecutara de arriba hacia abajo hasta finalizar.

Al escribir

```js
console.log("Hola mundo");
```

Suponiendo que nuestro archivo se llama `holamundo.js` podemos abrir una terminal en el mismo directorio que el archivo y ejecutar

```
node holamundo.js
```

Y observamos

![output de la terminal diciendo 'Hello World'](imagenes/03-helloworld.png)

### Sintaxis basica de javascript

> Esta sección es un pequeño resumen de sintaxis moderna de javascript (ES6), no es necesario revisar pero la idea es que resulte familiar a lo ya conocido por el alumno o que sirva de punto de partida para explorar

#### Declarando variables

Existen 3 formas de hacerlo

```js
var foo = "asd"; // Variable mutable de scope de funcion o global (No recomendado)
let foo = "asd"; // Variable mutable de scope de bloque
const foo = "asd"; // Variable inmutable de scope de bloque
```

> Para ver la diferencia de porque es recomendable `let` sobre `var` pueden leer este link de [let vs var](https://es.stackoverflow.com/questions/79809/cual-es-la-diferencia-de-usar-let-en-vez-de-var-en-javascript/79813)

En javascript no declaramos el tipo de dato al momento de crear variables, de hecho aunque no es para nada recomendable, el tipo de dato de la variable puede modificarse en tiempo de ejecucion.

El siguiente codigo es javascript valido y nos muestra los tipos de dato mas comunes

```js
let miVariable;
console.log("Type: ", typeof miVariable); // Type: undefined

miVariable = "asd";
console.log("Type: ", typeof miVariable); // Type: string

miVariable = 100;
console.log("Type: ", typeof miVariable); // Type: number

miVariable = 0.212312;
console.log("Type: ", typeof miVariable); // Type: number (no hay distincion de enteros)

miVariable = true;
console.log("Type: ", typeof miVariable); // Type: boolean

// Muchas cosas en javascript son 'object'
miVariable = \[1, 2, 3\]; // Arrays
console.log("Type: ", typeof miVariable); // Type: object

miVariable = {
	id: 1,
	nombre: "juan",
	apellido: "carlos",
	habilitado: true
}; // Objetos
console.log("Type: ", typeof miVariable); // Type: object

miVariable = null; // Null
console.log("Type: ", typeof miVariable); // Type: object

// Tambien podemos declarar variables definidas

let miVariableDefinida = miVariable;
const miConstanteDefinida = miVariable;
```

#### Bloques de control

Javascript tambien soporta los bloques de control similares a los que ya conocemos de otros lenguajes

- [witch](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Statements/switch)
- [while](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Statements/while)
- [for](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Statements/for)
- [if...else](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Statements/if...else)

#### Comparando variables

```js
// Operador '==' - Igualdad 'de valor' (no recomendable)
if (100 == "100") {
  console.log("Iguales (?) :thonk:");
}

// Operador '==' - Igualdad de valor y de tipo
if (100 === "100") {
  console.log("Esto no se ejecuta");
}
```

#### Valores Truty & Falsy de variables

Los valores en javascript se consideran verdaderos o falsos dependiendo de su contenido al momento de ser evaluado en un 'contexto booleano', esto es conveniente para checkeos.

| truthy                    | falsy              |
| ------------------------- | ------------------ |
| true                      | false              |
| 'false' (el string false) | 0                  |
| '0' (el string 0)         | '' (string vacio)  |
| () (funcion vacia)        | null               |
| \[\] (array vacio)        | undefined          |
| {} (objeto vacio)         | NaN (Not a number) |
| Los demas valores         |                    |

Algunos ejemplos

```js
let nombre = undefined;

// Usamos !! para negar dos veces e imprimir el valor booleano de la variable
// tambien podriamos haber escrito
//
// if(nombre){
//   console.log("true")
// }
//   console.log("false")
// }

console.log(!!nombre); // false

nombre = null;
console.log(!!nombre); // false

nombre = "";
console.log(!!nombre); // false

nombre = "Ricardo";
console.log(!!nombre); // true
```

#### El objeto global 'process' de Node

Node nos proporciona el objeto global [process](https://es.nodejs.org/docs/latest-v14.x/api/process.html#process_process) para obtener información e interactuar con el proceso actual.

Como `process` es un objeto global solo basta referenciarlo en nuestro programa para poder utilizarlo, sin embargo nuestro editor de texto a veces puede no reconocerlo. Si quisieramos ayudar el autocompletado del editor podríamos escribir:

```
 const process = require('process');
```

Utilizando process recuperar los argumentos de consola accediendo a proces.argv

![](imagenes/process-argv.png)

---

> Ejercicios
> Si querés resolver los ejercicios pensados para esta sección podes dirijirte a la hoja de [ejercicios-00](ejercicios/ejercicios-00.md)

---

## 1 - Funciones y asincronía en javascript

### Definición

Las funciones existen en casi todos los lenguajes de programación modernos, nos permiten encapsular comportamiento y reutilizar codigo. 

```js
function saludador(nombre) {
	return `Hola ${nombre}!`;
}

const greeter = function(name) {
return `Hello ${name}!`;
}

// Invocaciones
saludador("Ricardo");
greeter("Richard");
```

Desde **ES6** también declarar nuestras funciones con la sintaxis de *funciones flecha*

```js
const saludador = (nombre) => {
	return `Hola ${nombre}!`;
}

// Podemos comprimir quitando el return y los {}
const saludador = (nombre) => `Hola ${nombre}!`;

// Si solo recibe un parametro también podemos quitar el () 
const saludador = nombre => `Hola ${nombre}!`;

// Si no recibe parametros tenemos que usar ()
const saludador = () => `Hola Extraño!`;

```

### Funciones como first class citizens

En javascript las funciones van un paso mas alla, se consideran 'first-class citizen' (o ciudadanos de primera clase), esto quiere decir que son tratadas como cualquier otra variable. Por ejemplo, una funcion puede recibir otra funcion como parametros, retornar una funcion y que esta sea luego asignada a una variable.

```js
// Asignando funciones a variables
const f1 = function foo() { console.log("foo"); };
const f2 = function () { console.log("anonima"); };
const f3 = () => console.log("anonima");

// Declarando funciones y ejecutandolas inmediatamente (se asigna el resultado)
const hola = function () { return "hola"} ()
const chau = ( () => "chau" )() // En este caso tenemos que agregar parentesis extras

// Funciones como parametros
const sumar = (a,b) => a + b;
const operar = (operacion, n1, n2) => console.log(operacion(n1,n2))
operar(sumar, 1, 2) // Imprime: 3

// Funciones que retornan funciones (también llamadas thunks)
const restar = (n1) => (n2) => console.log(n1 - n2)
restar(10)(8) // Imprime: 2

```

### Clausuras

Un detalle a mencionar es que javascript, a diferencia de lenguajes como java, no ofrece una manera nativa de marcar funciones 'privadas'. Pero nos permite simular ese comportamiento mediante [clausuras](https://developer.mozilla.org/es/docs/Web/JavaScript/Closures)

Una clausura  es una funcion que permite acceder al ámbito de una función exterior desde una función interior. En JavaScript, las clausuras se crean cada vez que una función es creada.

Veamos este ejemplo

```js
const saludar = (() => {
  const componerNombre = (n, a) => `${n} ${a}`;
  
  return (nombre,apellido) => {
  	const nombreApellido = componerNombre(nombre, apellido);
	console.log(`Hola ${nombreApellido}`)  
  };
})(); 

saludar("Ricardo", "Sanchez");  
```

Estamos definiendo una función y luego ejecutandola inmediatamente, esta retorna otra funcion que toma `nombre` y `apellido` de parametro y se asigna a la variable `saludar`. Ahora, desde la funcion `saludar` estamos haciendo referencia a la funcion interna `componerNombre` pero esta no puede ser accedida de forma externa, logrando un resultado similar al de las funciones privadas.

### Asincronia en Javascript

El runtime de Javascript solo puede ejecutar una sola cosa a la vez, es un lenguaje de programación single-threaded (un hilo) y por lo tanto solo puede procesarse de a una instrucción.

Esto nos impone una limitante al tratar de realizar operaciones que se extienden en el tiempo como consultar apis. Si nuestra función demora estaremos bloqueando el hilo principal y por lo tanto nada mas podra ejecutarse.

Por ejemplo, desde la consola de desarrollador de chrome podemos ejecutar `while(true){}` y de esta manera tildar completamente la tab ya que no desocupamos el hilo para que la página siga funcionando.

![](imagenes/chrometildado.gif)

Ahora, acabamos de decir que nuestro javascript ejecuta en un unico hilo, por lo que no podemos recurrir a la programación **paralela** para solucionar nuestros problemas pero si a la programación **concurrente**

![](imagenes/concurrency.png)

Pero nosotros no ejecutamos solo javascript, ejecutamos javascript en un navegador o sobre nodejs y estos poseen un modelo de concurrencia basado en un "loop de eventos". Si bien este modelo es diferente al que estamos acostumbrados en lenguajes como Java y existen varios recursos dedicados a [explicar su funcionamiento](https://www.youtube.com/watch?v=8aGhZQkoFbQ) de momento nos alcanza con saber que es la estrategia para resolver tareas concurrentes.

// promises
// then catch
// async await

## 2 - Manipulando objetos y arrays

#### Objetos

// TODO

#### Operaciones sobre arrays

// TODO

#### Desestructuracion

// TODO

## 3 - Potenciando node

#### NPM

Hasta ahora solamente hemos usado las herramientas provistas por NodeJS pero nos estamos perdiendo de una de las ventajas mas grandes de javascript, su extensa comunidad y la gran cantidad de librerias de terceros a nuestra disposición.

Para ayudarnos a encontrar y administrar estas dependencias NodeJS, por defecto, incluye un sistema de gestión de paques llamado NPM (Node Package Manager)

Solo teniendo node instalado, desde una terminal, podemos acceder a el

```bash
$ npm -v
```

Todos nuestros ejercicios implicaban crear un archivo con extensión `.js` y ejecutarlo mediante el comando `node archivo.js`. Si bien puede ser suficiente para scripts sencillos, para desarrollar aplicaciones complejas que necesitan de librerías externas en versiones especificas empezamos a tener problemas.

Utilizando npm podemos generar una estructura de proyecto para nuestra aplicación mediante el comando `npm init`

```bash
$ mkdir mi-proyecto && cd mi-proyecto // Creamos una carpeta y navegamos dentro
$ npm init
```

Al ejecutar el comando `init` la utilizadad de npm nos guiará paso a paso en la creación de un archivo `package.json`.

![](imagenes/04-npm-init.png)

En el queda descrito el nombre del proyecto, la versión y otras caracteristicas de las cuales, sin duda la mas importante, es el registro de las dependencias necesarias para ejecutar nuestro código.

#### Creando un script de inicializacion de nuestro proyecto
Si revisamos nuestro package.json vemos que se autogenero un tag `main` con el siguiente valor que simboliza el punto de entrada de nuestra aplicacion 

```json
"main": "index.js"
```
> Importante:
> `npm init` no genero ningun archivo index.js asi que vas a tener que generarlo o cambiar el nombre al que tengas

Antes para ejecutar nuestra aplicacion ejecutabamos el comando `node index.js`, al tener `main` definido podemos solo escribir `node .` y dejar que el punto de entrada se levante del `package.json`. Ahora desde npm tambien podemos definir `scripts` de ejecucion.

Para crear script solo hay que asignarle una nombre, seguido del comando de consola a ejecutar, dentro de la key `scripts` del `package.json`. Luego para ejecutarlo desde la terminal lanzamos

```bash
$ npm run nombre-de-script
```

Generalmente en el package json se agrega un script con el nombre `start` que ejecuta nuestra aplicacion, por ejemplo

```json
{
	"name": "mi-proyecto",
	"version": "1.0.0",
	"description": "Mi primer proyecto usando npm",
	"main": "index.js",
	"scripts": {
		"start": "node index.js"
	},
	"author": "Leandro Amarillo",
	"license": "ISC"
}
```

De esta manera ejecutar `npm run start` lanza nuestra apliacion.

Si bien este es un caso bastante trivial, utilizar scripts empieza a volverse muy util para proyectos que cuenten con tests (podriamos crear un script `test` que los ejecute),  cuando queremos modificar argumentos (ejemplo: variables de entorno) o si durante el desarrollo queremos utilizar alguna herramienta como [nodemon](https://www.npmjs.com/package/nodemon) (que veremos mas adelante).

#### Agregando librerias de terceros

Como ya mencionamos, existe una gran cantidad de librerias de terceros listas para ser utilizadas en nuestro código, por ejemplo, podemos ver algunas de ellas en el repositorio [awesome-javascript](https://github.com/sorrycc/awesome-javascrip) que se dedica a recolectar y catalogarlas.

Para agregar una libreria, desde una terminal en el directorio donde se encuentra el `package.json`, debemos ejecutar

```bash
$ npm i nombre-de-libreria
```

Luego de agregar una librería al proyecto el `package.json` habrá agregado una entrada dentro de la key `dependencies`.

Algunas librerias no son necesarias para ejecutar la aplicación pero si para facilitar el desarrollo (ej: framework de testing unitario) y para esto npm tambien nos deja instarlarlas utilizando

```bash
$ npm i nombre-de-libreria -D
```

Estas dependencias tambien se agregan al `package.json` pero dentro de la entrada `devDependencies`

#### El directorio node-modules

Si nos descargamos un proyecto que utiliza npm, por ejemplo desde github, gracias a este `package.json` simplemente tenemos que ejecutar `npm i` para descargar las dependencias requeridas. Estas dependencias se guardan dentro de un directorio llamado `node-modules`, si es la primera vez que se descargan tambien se generá un archivo denominado `package-lock.json` el cual indica las versiones de los paquetes que se descargaron y si este esta versionado permite que todos los que descarguen el proyecto utilicen las mismas versiones de las dependecias.

#### Importando módulos en nuestro código

NodeJS utiliza la sintaxis `require('nombre-del-modulo')` para cargar nuestras dependencias, esta función devuelve un objeto que contiene las funcionalidades que el modulo exporta es por esto que si, por ejemplo, estamos importando el modugo `fs` (file system) incluido en nodejs se suele hacer de la siguiente manera

```js
const fs = require("fs");
```

La misma sintaxis aplica a las librerias de terceros, por ejemplo para utilizar la librería [dayjs](https://github.com/iamkun/dayjs) que nos facilita el manejo de fechas primero ejecutamos `npm i dayjs` para agregar y descargar la dependecia y luego para utilizarla solo hacemos

```js
const dayjs = require("dayjs");
```

##### require (commonJS) vs import (ES6)
 Por default NodeJS utiliza la sintaxis de commonJS, para utilizar la sintaxis de ES6 que utilizaremos cuando veamos react a partir de NodeJS v12 podemos modificar el `package.json` agregando la key `"type": "module"` luego podemos reemplazar nuestros imports a la forma
 
 ```js 
 import dayjs from 'dayjs'
```

 Existen otras diferencias a la hora de generar nuestros propios modulos y detalles de implementacion de como se cargan que no vienen al caso en una guia introductoria. A partir de este momento se utilizara la sintaxis de ES6 para mantener la familiaridad para cuando veamos react a futuro.

## 4 - API usando NodeJS y Express

#### Express

#### Reiniciando nuestro servidor local cuando se modifican archivos

//TODO
