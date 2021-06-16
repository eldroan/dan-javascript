## Ejercicios - Funciones y asincronía en javascript

> Esta guía esta desarrollada en base a los conceptos presentados en la seccion [' 1 - Funciones y asincronía en javascript'](../README.md#1---funciones-y-asincronía-en-javascript)

#### 0 - Una calculadora como excusa para escribir funciones

Escribir un programa que reciba tres parámetros. El primer parámetro una palabra correspondiente a la operación a realizar que puede ser `sumar`, `restar`,  `multiplicar` o `dividir`, el segundo y tercer parametro serán los números a operar.

Ejemplo:
```bash
$ node calculadora.js sumar 2 10
```

Si recibimos una operación invalida imprimiremos el mensaje `La operacion ${arg2} no es válida` donde `${arg2}` es el nombre de la operación invalida que pasamos por argumento.

Si la operación lanza un error (ej: división por 0) mostrar el mensaje `La operación ${arg2} no se pudo realizar para los parametros ${arg3} y ${arg4}` donde `${arg2}` es el nombre de la operación, `${arg3}` es el primer numero y `${arg4}` es el segundo numero.

Si la operación es exitosa mostrar el mensaje `El resultado fue: ${resultado}`


---

#### 1 - La misma calculadora, pero interactiva!

Modificar el codigo del ejercicio anterior para que en lugar de tomar los parametros desde los argumentos del programa se los pregunte al usuario y lea el input desde la consola.

Ejemplo:
```bash
Que operación desea realizar? sumar
Cuál es el primer número? 2
Cuál es el segundo número? 10
```

Una vez de mostrar el resultado de la operación (o el error) mostrará el mensaje

```bash
Desea realizar otra operación?
```

Si el usuario responde `no` finalizará la aplicación pero si el usuario responde `si` volveremos a pedir los parámetros y volver a ejecutar hasta que el usuario decida responder `no`.

##### Código de ayuda

Para leer los inputs podemos utilizar el módulo [readline](https://nodejs.org/api/readline.html) de node

Readline primero requiere inicializarlo de la siguiente manera antes de poder usarlo

```js
import readline from 'readline' // Recordar modificar extensión a .mjs para que esto funcione

const rl = readline.createInterface({
	input: process.stdin,
	output: process.stdout
});
```

Luego podemos usar [rl.question](https://nodejs.org/api/readline.html#readline_rl_question_query_options_callback) para imprimir un mensaje en consola y leer una linea de input. Esta api utiliza callbacks, si queremos convertilo a promesas podemos definir este helper

```js
const preguntar = pregunta => {
	return new Promise((resolve, reject) => {
		rl.question(pregunta, respuesta => resolve(respuesta));
	});
};
```

Y luego podemos utilizarlo de la siguiente manera

```js
let operacion = await preguntar("Que operación desea realizar? ")
```

Al utilizar readline nuestra aplicación no se cerrara hasta cerrar el input stream haciendo `rl.close()` o también podemos apoyarnos en el objeto process para cerrar la aplicacón ejecutando `process.exit()`

---

#### 2 - "Prométeme que me recordaras." - Javascript (17 de Junio 2015) 

Escriba un programa que permita guardar recordatorios. Al comenzar se le pedirá al usuario que ingrese un mensaje para su recordatorio y cuantos segundos mas tarde desea ver el recordatorio.

Ejemplo:

```
Ingrese un mensaje para su recordatorio: Aprender javascript
Ingrese en cuanto tiempo (segundos) desea recibir el recordatorio: 10 
```

Luego de ingresar ambos valores el programa deberá preguntar

```
Recordatorio creado. Desea agregar otro recordatorio? (si/no)
```

A esta altura el recordatorio se creará y cuando el tiempo previsto se cumpla deberá imprimirse en pantalla `Recordatorio: ${mensaje}` con `${mensaje}` siendo el texto que seteamos para ese recordario.

Si el usuario responde  `si`  a la pregunta volverá a completar los datos y se creara un nuevo recordatorio. Si el usuario selecciona `no`  y no quedan recordatorios pendientes el programa finalizará pero si aún quedan recordatorios se mostrará el mensaje

```js
Esperando recordatorios pendientes...
```

Y luego de que todos los recordatorios terminen de mostrarse en pantalla la app se cerrará.

Para la resolución del problema podes utilizar las apis de [Promise.all()](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)  y de [setTimeout](https://nodejs.org/en/docs/guides/timers-in-node/#when-i-say-so-execution-settimeout). Ademas,  podés utilizar el codigo de ayuda del ejercicio anterior.