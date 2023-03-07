## Nuevas Features

ES6 incluye las siguientes features:

- **[let + const (Block Scoping)](#let--const)**
- **[arrows =>](#arrows)**
- **[classes](#classes)**
- **[object literals mejorados](#enhanced-object-literals)**
- **[template strings](#template-strings)**
- **[destructuring](#destructuring)**
- **[default + rest + spread](#default--rest--spread)**
- [iterators + for..of](#iterators--forof)
- [generators](#generators)
- [unicode](#unicode)
- [modules](#modules)
- [module loaders](#module-loaders)
- [map + set + weakmap + weakset](#map--set--weakmap--weakset)
- [proxies](#proxies)
- [symbols](#symbols)
- [subclassable built-ins](#subclassable-built-ins)
- **[promises](#promises)**
- [math + number + string + array + object APIs](#math--number--string--array--object-apis)
- [binary and octal literals](#binary-and-octal-literals)
- [reflect api](#reflect-api)
- [tail calls](#tail-calls)
- [Optional Chaining](#optional-chaining)

## ECMAScript 6 Features

### Let + Const

`let` es el nuevo `var`. Sólo que let tiene un scope distinto, este está declarado sólo dentro del `bloque` donde aparece y no dentro del scope (por ejemplo si uso `let` dentro de un `for` no voy a poder ver esa variable afuera del mismo, está bien claro [acá](http://stackoverflow.com/questions/762011/let-keyword-vs-var-keyword-in-javascript)). `const` es para declarar variables inmutables o sea que no pueden cambiar. Si queremos asignar un nuevo valor a una variable declara con `const` vamos a obtener un Error.

```js
function f() {
  {
    let x;
    {
      // okay, block scoped name
      const x = "sneaky";
      // error, const
      x = "foo";
    }
    // error, already declared in block
    let x = "inner";
  }
}
```
### Notas viendo la lecture:
    *Todo es const... hasta que necesite lo contrario*

    *var no se usa mas!!*

---
---

Más Info: [let statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let), [const statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)



### Arrows

Arrows (o flechas) son una forma de abreviar la declaración de una función y utiliza la sintaxis `=>` (está inspirada en sintaxis similares de C#, Java 8 y CoffeeScript). Estas soportan cuerpos que sean statements (ifs, fors, etc..) y también cuerpos que retornen el resultado de una expresion. A diferencia de las funciones normales, las funciones __arrows comparten el mismo `this` que el código que las rodea__.

```js
// Cuerpos con Expresiones
var pares = impares.map(v => v + 1);
var nums = pares.map((v, i) => v + i);

// Cuerpos con Statements
nums.forEach(v => {
  if (v % 5 === 0)
    cincos.push(v);
});

// this
var bob = {
  _name: "Bob",
  _friends: [],
  printFriends() {
    this._friends.forEach(f =>
      console.log(this._name + " knows " + f));// this es bob por la arrow f
  }
}
```
## IMPORTANTE:
Las arrow function toman el this del lugar donde fueron definidas, es decir hacen un auto bind.
Con las arrow function le decimos adios al metodo Bind!!

## Notas viendo la lecture:
```javascript
function sumar (a, b) {
    const resultado = a + b;
    return resultado
}
```
#### Esto se va a traducir a esto en arrow function: 
```javascript
const sumar = (a, b) => {
    const resultado = a + b;
    return resultado
}
```
#### Aun mas resumido:
Si la arrow funcion tiene una sola linea , y en esa unica linea retorna algo, podemos obviar el return y escribirlo asi
```javascript
const sumar = (a, b) => a + b;
```
## Tambien nos sirve para expresiones:
```javascript
const arr = [1,2,3,4,5,6,7,8,9]
const pares = arr.filter(function (num){
    //la callback del metodo filter retorna una condicion
    return num%2 === 0;
})
```
Vamos a escribir asi:
```javascript
const arr = [1,2,3,4,5,6,7,8,9]
const pares = arr.filter((num) => {
    return num%2 === 0
    };
)
```
Y como tengo una sola linea: Podemos obviar las {} y eliminamos el 'return'
```javascript
const arr = [1,2,3,4,5,6,7,8,9]
const pares = arr.filter((num) =>  num%2 === 0)

```
Y que es lo mejor???? *Lo que entiendas hasta hoy!!!*

### En conclusion:
    Resume el codigo
    Elimina el Bind
---


Más información: [MDN Arrow Functions](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

### Classes

Las clases en ES6 son simplemente syntax sugar sobre el patrón de prototipado de objetos. Tener una forma particular de declarar clases, hace que sea más fácil de usar y mejora la interoperabilidad. Las clases soportan la herencia basada en prototipos, llamadas a super, instance y métodos estáticos y constructores.

```js
class SkinnedMesh extends THREE.Mesh {
  constructor(geometry, materials) {
    super(geometry, materials);

    this.idMatrix = SkinnedMesh.defaultMatrix();
    this.bones = [];
    this.boneMatrices = [];
    //...
  }
  update(camera) {
    //...
    super.update();
  }
  get boneCount() {
    return this.bones.length;
  }
  set matrixType(matrixType) {
    this.idMatrix = SkinnedMesh[matrixType]();
  }
  static defaultMatrix() {
    return new THREE.Matrix4();
  }
}
```



## Notas de la lecture:
Lo importante es aprender a usar el constructor de clase

```javascript
class Persona {
  constructor(nombre, apellido) {
    this.nombre = nombre;
    this.apellido = apellido;
  }
  getNombre(){
    this.nombre;// Esta funcion lo que hace es retornar el nombre
  }
}
 const persona1 = new Persona('Jorge', 'Vega');
 console.log(persona1)// --> Persona{ nombre: 'Jorge, apellido: 'Vega'}
 console.log(persona1.getNombre());//---->> 'Jorge'
```
*Lo que hacemos es crear una clase con el constructor y asignarle una funcion que retorne el nombre, consologueamos y nos devuelve el objeto y la invocacion de la funcion*

## Ahora vamos a hacer la herencia de esa clase Persona
Vamos a crear la clase 'Empleado' y un empleado antes de ser empleado es Persona
```javascript
class Empleado extends Persona {
  constructor(nombre,apellido,cargo){// Se le pasan parametros para crear un Empleado
    super(nombre, apellido) // super se usa para llamar al constructor de Persona.
    this.cargo = cargo; // y aca agregamos el cargo del Empleado, que ya tiene nom y apellido
  }
}
const empleado1 = new Empleado('Pedro', 'Casillas','Jefe de ventas');
console.log(empleado1) //--> Empleado{nombre:'Pedro, apellido:'Casillas',cargo:'Jefe de ventas'}
console.log(empleado1.getNombre())//--->> Pedro
```
*La herencia tambien hereda los metodos que creamos en la clase padre.En este caso getNombre*


Más info: [MDN Classes](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes)

### Object Literals Mejorados

Ahora los Object Literals se extendedieron para setear el prototipo durante su construcción, atajos para cuando hacemos una asignación de este tipo: `propiedad: propiedad`, definimos métodos, cuando hacemos llamadas a super, y al computar nombres de propiedades en una expresión. Todo esto junto mejora el proceso de diseño orientado a objetos ya que trabaja en sinergía con las mejoras en las clases antes mencionadas.

```js
var obj = {
    // __proto__
    __proto__: theProtoObj, //extiende el prototipo
    propiedad, // atajo para propiedad:propiedad
    // Methods
    toString() {
     // Super calls
     return "d " + super.toString();
    },
    // Computed (dynamic) property names
    [ 'prop_' + (() => 42)() ]: 42
};
```

Más Info: [MDN Grammar and types: Object literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types#Object_literals)

### Template Strings

Los Template Strings son una syntax sugar para la construcción de strings. Es parecido a la interpolación de stings de Perl, Python y otros lenguajes.

```js
// Basic literal string creation
`In JavaScript '\n' is a line-feed.`

// Multiline strings
`In JavaScript this is
 not legal.`

// String interpolation
var name = "Bob", time = "today";
`Hello ${name}, how are you ${time}?`

// Construct an HTTP request prefix is used to interpret the replacements and construction
POST`http://foo.org/bar?a=${a}&b=${b}
     Content-Type: application/json
     X-Credentials: ${credentials}
     { "foo": ${foo},
       "bar": ${bar}}`(myOnReadyStateChangeHandler);
```

Más Info: [MDN Template Strings](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/template_strings)

### Destructuring

Las estructuras se pueden desestructurar para poder seleccionar valores
usando patrones de matcheo, con soporte para arreglos y objetos. Esto funciona igual que buscar una propiedad de un objeto `foo['bar']` en el sentido que ambos son `fail-soft`, es decir, que producen un `undefined` cuando algo no se encuentra.

```js
// list matching
var [a, , b] = [1,2,3];

// object matching
var { op: a, lhs: { op: b }, rhs: c }
       = getASTNode()

// object matching shorthand
// binds `op`, `lhs` and `rhs` in scope
var {op, lhs, rhs} = getASTNode()

// Can be used in parameter position
function g({name: x}) {
  console.log(x);
}
g({name: 5})

// Fail-soft destructuring
var [a] = [];
a === undefined;

// Fail-soft destructuring with defaults
var [a = 1] = [];
a === 1;
```
## Notas de la lecture:
Vamos a poder extraer informacion de arreglos y objetos, y guardarlos en variables para utilizarlos.
Ejemplo:

### Destructuracion con objetos:
#### Importante: Necesitamos conocer si o si el nombre de las propiedades a extraer
```javascript
const Persona{
  nombre = 'German',
  apellido = 'Montenegro',
  direccion = 'Santa fe 1555',
  cp = '3400',
  mail = 'german123@gmail.com',
}
// Lo que quiero es extraer solo unas propiedades de ese objeto Persona:
// se crea una variable que contenga solo esas propiedades:
const {nombre, apellido, mail} = objeto1

//Esto devuelve una variable (objeto1) con un objeto:
console.log(objeto1)//->{nombre ='German', apellido ='Montenegro', mail ='german123@gmail.com'}

```
Tambien si hacemos una destructuracion con una funcion seria asi:
```javascript
const Persona{
  nombre = 'German',
  apellido = 'Montenegro',
  direccion = 'Santa fe 1555',
  cp = '3400',
  mail = 'german123@gmail.com',
}
function cualquiera(obj){
  const {nombre, apellido, mail} = obj
  return{
    nombre,
    apellido,
    mail,
  };
}
console.log(cualquiera(obj))//-->> //->{nombre ='German', apellido ='Montenegro', mail ='german123@gmail.com'}
```
La destructuracion podemos hacerla directamente al llamar al objeto, pasando como parametro las propiedades que queremos que extraiga del objeto principal
Ejemplo:
```javascript
function cualquiera({nombre, apellido, mail}){// aca le pasamos por parametro las propiedades
  return{// y retoranamos directamente 
    nombre,
    apellido,
    mail,
  };
}
//esta funcion toma como referencia el parametro que se le pasa al invocar a la funcion
//                      ||    
//                      \/   
console.log(cualquiera(obj))//-->> //->{nombre ='German', apellido ='Montenegro', mail ='german123@gmail.com'}
```
## Con un array es algo similar:
### Importante: Lo vamos a usar generalmente para Array pequeños, donde tengamos certeza de lo que hay dentro
*Ejemplo:*

```javascript
const arr = ['facundo', 'Leandro', 'Liliana']
//             /          /        /
//            /          /        /
const [persona1, persona2, persona3] = arr;
```
*Otro ejemplo:*
```javascript
const arr = ['Valor X', () => {}]// un valor x y una funcion
//uso destructuracion para guardarme los dos elementos en dos variables distintas
const [valor, funcion] = arr;
// Ahora si hago console log vemos que podemos llamarlas por separado
console.log(valor)//-->> Valor X
console.log(funcion)//-->> ()=>{}
//Esto se usa para no estar llamando a los elementos asi:
arr[0]
arr[1]
```

Más Info: [MDN Destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

### Default + Rest + Spread

Las declaraciones de funciones pueden tener argumentos que defaultean a  un valor si no son declarados. También se puede transformar un arreglo en argumentos consecutivos. Y al reves, o sea podemos bindear los últimos elementos de los argumentos como si fuera un sólo arreglo.

```js
function f(x, y=12) {
  // y is 12 if not passed (or passed as undefined)
  return x + y;
}
f(3) == 15
```

```js
function f(x, ...y) {

  // y is an Array
  return x * y.length;
}
f(3, "hello", true) == 6
```

```js
function f(x, y, z) {
  return x + y + z;
}
// Pass each elem of array as argument
f(...[1,2,3]) == 6
```

## Notas de la lecture:
### Spread:
Sirve para llamar a un array existente, o para concatenarlo con mas elementos o mas arrays
se lo llama con 3 puntos (...)
Ejemplo 1: llamando a un array ya existente
```javascript
const arr1 = [1,2,3];
const nuevoArray = [...arr1]// los tres puntitos se leen 'los elementos de:'
// y si consologueo:
console.log(nuevoArray)//-->> [1,2,3]
```
Tambien puedo añadir elementos a ese arreglo
Ejemplo:
```javascript
const arr1 = [1,2,3];
const arrAñadido = [...arr1,4,5,6];
console.log(arrAñadido)//-->>[1,2,3,4,5,6]
// Otro ejemplo
const arrAñadido2 = [0,1,2,...arr1,7,8,9];
console.log(arrAñadido2)//-->>[0,1,2,1,2,3,7,8,9];
```

Tambien puedo concatenar Arreglos
Ejemplo:
```javascript
const arr1 = [1,2,3];
const arr2 = [4,5,6];
const arrConcatenado = [...arr1,...arr2];
console.log(arrConcatenado)//-->>[1,2,3,4,5,6]
```

## Tambien funciona con Objetos:
Ejemplo:
```javascript
const persona = {// tengo un objeto de persona
  nombre: 'German',
  edad: 29,
}
const personaConApellido ={//y quiero hacer una copia con las mismas prop y agregarle apellido 
  ...persona
  apellido:'Montenegro',
}
// Consologueamos
console.log(personaConApellido)//-->{nombre: 'German',edad: 29, apellido:'Montenego'}
```

### Importante: Se puede modificar una propiedad que se extrajo de person
Ejemplo:
```javascript
const personaConApellido ={
  ...persona
  apellido:'Montenegro',
  edad: 28, // se modifica la propiedad
}
console.log(personaConApellido)//-->{nombre: 'German',edad: 23, apellido:'Montenego'}
```
*Si tiene metodos tambien los trae*


Más Info: [Default parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters), [Rest parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters), [Spread Operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)

### Iterators + For..Of

Un objeto es un iterador cuando sabe como acceder a una colección de items de a uno, mientras mantiene su posición dentro de esa secuencia. En ES6 un iterador es cualquier cosa que provea un método `next()` que retorn el próximo item en la secuencia.

También se generalizó el `for...in` para poder usar `for...of` en iteradores.

```js
let fibonacci = {
  [Symbol.iterator]() {
    let pre = 0, cur = 1;
    return {
      next() {
        [pre, cur] = [cur, pre + cur];
        return { done: false, value: cur }
      }
    }
  }
}

for (var n of fibonacci) {
  // truncate the sequence at 1000
  if (n > 1000)
    break;
  console.log(n);
}
```

Más info: [MDN for...of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)

### Generators

Los iteradores son herramientas muy útiles, hay que tener mucho cuidado cuando los programamos porque necesitan mantener internamente su estado todo el tiempo. Los generadores nos proveen una alternativa poderosa: te dejan definir un algoritmo iterativo escribiendo una función que mantenga su propio estado.

```js
function* idMaker(){
  var index = 0;
  while(true)
    yield index++;
}

var gen = idMaker();

console.log(gen.next().value); // 0
console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
// ...
```

Más info: [MDN Iteration protocols](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols)

### Unicode

Hicieron adiciones para mejorar el soporte con Unicode.

```js
// same as ES5.1
"𠮷".length == 2

// new RegExp behaviour, opt-in ‘u’
"𠮷".match(/./u)[0].length == 2

// new form
"\u{20BB7}"=="𠮷"=="\uD842\uDFB7"

// new String ops
"𠮷".codePointAt(0) == 0x20BB7

// for-of iterates code points
for(var c of "𠮷") {
  console.log(c);
}
```

Más Info: [MDN RegExp.prototype.unicode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/unicode)

### Modules

Ahora Javascript soporta módulos de forma nativa (antes era mediante `CommonJS`), es muy parecido ya que están basados en la filosofía de lo que ya veniamos usando.

```js
// lib/math.js
export function sum(x, y) {
  return x + y;
}
export var pi = 3.141593;
```

```js
// app.js
import * as math from "lib/math";
alert("2π = " + math.sum(math.pi, math.pi));
```

```js
// otherApp.js
import {sum, pi} from "lib/math";
alert("2π = " + sum(pi, pi));
```

Ahora podemos distinguir los __named exports__, que son básicamentes todos los que exporten una variable con un nombre, por ejemplo: `export var pi = 3.14;`. Podemos tener muchos de estos por archivo.
También existe el __Default Export__: Sólo puede haber _uno_ por archivo, este es más parecido a la vieja forma de exportar. Generalmente lo usamos cuando, al importar, queremos que esté _todo_ dentro de un objeto y no importar _varios_ objetos separados.

```js
// lib/mathplusplus.js
export * from "lib/math";
export var e = 2.71828182846;
export default function(x) {
    return Math.log(x);
}
```

```js
// app.js
import ln, {pi, e} from "lib/mathplusplus";
alert("2π = " + ln(e)*pi*2);
```

Más info: [import statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import), [export statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export)

### Map + Set + WeakMap + WeakSet

Nuevas Estructuras de datos. En general basadas en estructuras muy usadas en otros lenguajes.

```js
// Sets
var s = new Set();
s.add("hello").add("goodbye").add("hello");
s.size === 2;
s.has("hello") === true;

// Maps
var m = new Map();
m.set("hello", 42);
m.set(s, 34);
m.get(s) == 34;

// Weak Maps
var wm = new WeakMap();
wm.set(s, { extra: 42 });
wm.size === undefined

// Weak Sets
var ws = new WeakSet();
ws.add({ data: 42 });
// Because the added object has no other references, it will not be held in the set
```

Más Info: [Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map), [Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set), [WeakMap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakMap), [WeakSet](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/WeakSet)

### Subclassable Built-ins

En ES6, objetos nativos como `Array`, `Date` y elementos del `DOM` pueden ser heredados por una subclase.

Object construction for a function named `Ctor` now uses two-phases (both virtually dispatched):

- Call `Ctor[@@create]` to allocate the object, installing any special behavior
- Invoke constructor on new instance to initialize

The known `@@create` symbol is available via `Symbol.create`.  Built-ins now expose their `@@create` explicitly.

```js
// Pseudo-code of Array
class Array {
    constructor(...args) { /* ... */ }
    static [Symbol.create]() {
        // Install special [[DefineOwnProperty]]
        // to magically update 'length'
    }
}

// User code of Array subclass
class MyArray extends Array {
    constructor(...args) { super(...args); }
}

// Two-phase 'new':
// 1) Call @@create to allocate object
// 2) Invoke constructor on new instance
var arr = new MyArray();
arr[1] = 12;
arr.length == 2
```

### Math + Number + String + Array + Object APIs

Se agregaron cosas nuevas en las librerías nativas, incluyendo librerías matemáticas, funciones para convertir arreglos, funciones para trabajar Strings, y Object.assign para copiar objetos.

```js
Number.EPSILON
Number.isInteger(Infinity) // false
Number.isNaN("NaN") // false

Math.acosh(3) // 1.762747174039086
Math.hypot(3, 4) // 5
Math.imul(Math.pow(2, 32) - 1, Math.pow(2, 32) - 2) // 2

"abcde".includes("cd") // true
"abc".repeat(3) // "abcabcabc"

Array.from(document.querySelectorAll('*')) // Returns a real Array
Array.of(1, 2, 3) // Similar to new Array(...), but without special one-arg behavior
[0, 0, 0].fill(7, 1) // [0,7,7]
[1, 2, 3].find(x => x == 3) // 3
[1, 2, 3].findIndex(x => x == 2) // 1
[1, 2, 3, 4, 5].copyWithin(3, 0) // [1, 2, 3, 1, 2]
["a", "b", "c"].entries() // iterator [0, "a"], [1,"b"], [2,"c"]
["a", "b", "c"].keys() // iterator 0, 1, 2
["a", "b", "c"].values() // iterator "a", "b", "c"

Object.assign(Point, { origin: new Point(0,0) })
```

Más info: [Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number), [Math](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math), [Array.from](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from), [Array.of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/of), [Array.prototype.copyWithin](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/copyWithin), [Object.assign](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)

### Binary y Octal Literals

Dos nuevas formas literales agregadas para binario (`b`) y octal (`o`).

```js
0b111110111 === 503 // true
0o767 === 503 // true
```

### Promises

Promises es una librería para mejorar la programación asíncrónica. Las Promises son una representación de tipo first-class de un valor que va a estar disponible en el futuro. Esto también ya existia con otras librerías de terceros.

```js
function timeout(duration = 0) {
    return new Promise((resolve, reject) => {
        setTimeout(resolve, duration);
    })
}

var p = timeout(1000).then(() => {
    return timeout(2000);
}).then(() => {
    throw new Error("hmm");
}).catch(err => {
    return Promise.all([timeout(100), timeout(200)]);
})
```

Más info: [MDN Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)

### Tail Calls

Se puede implementar llamadas recursivas sin tener que agregar un un frame al `call stack` haciendo que sea segura la ejecución de una función recursiva (sin temer por el stack overflow).

```js
function factorial(n, acc = 1) {
    'use strict';
    if (n <= 1) return acc;
    return factorial(n - 1, n * acc);
}

// Stack overflow in most implementations today,
// but safe on arbitrary inputs in ES6
factorial(100000)
```

> Podemos ver una lista de features más detallada y comparada con la versión anterior [aquí](http://es6-features.org/)

### Optional Chaining

El operador de encadenamiento opcional `?.` permite leer el valor de una propiedad ubicada dentro de una cadena de objetos conectados sin tener que validar expresamente que cada referencia en la cadena sea válida. El operador `?.` funciona de manera similar a el operador de encadenamiento `.` , excepto que en lugar de causar un error si una referencia es `null` o `undefined`, la expresión hace una short-circuit evaluation (`la evaluacion del segundo termino solo se efectua si el primero no permite definir un resultado ej: (true ||false)---> da verdadero sin siquiera pasar por false`) con un valor de retorno de `undefined`. Cuando se usa con llamadas a funciones, devuelve `undefined` si la función dada no existe.
Esto da como resultado expresiones más cortas y simples cuando se accede a propiedades encadenadas dónde existe la posibilidad de que falte una referencia. También puede ser útil al explorar el contenido de un objeto cuando no hay una garantía conocida de qué propiedades se requieren.

```js
const adventurer = {
  name: 'Alice',
  cat: {
    name: 'Dinah'
  }
};

const dogName = adventurer.dog?.name;
console.log(dogName);
// expected output: undefined

console.log(adventurer.someNonExistentMethod?.());
// expected output: undefined

```

## Compatibilidad

Para poder utilizar la sintaxis y las nuevas funcionalidad de ES6 en los motores no compatibles, vamos a utilizar [Babel.js](https://babeljs.io/)

Para instalarlo:

```bash
# install the cli and this preset
npm install --save-dev @babel/core @babel/cli

# make a .babelrc (config file) with the preset
npm install @babel/preset-env 
echo '{ "presets": ["@babel/preset-env"] }' > .babelrc

# create a file to run on
echo 'console.log([1, 2, 3].map(n => n + 1));' > index.js

# run it
./node_modules/.bin/babel-node index.js
```

De esa forma vamos a poder transformar un archivo y lo tenemos que hacer manualmente. Si queremos que sea automático tenemos muchísimas opciones.
Veamos algunas en la página de [babel](https://babeljs.io/docs/setup/) y elijamos el setup que más nos guste.