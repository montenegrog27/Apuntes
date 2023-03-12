# BUNDLERS
## Modulos:

# 1_ module.exports {}

Tenemos dos moduloes, 'funciones.js' e 'index.js', para poder usar funciones declaradas en el modulo funciones.js, en nuestro index.js, es necesario utilizar el metodo .exports de los module  
Ej:
### funciones.js
```javascript
const suma = (a , b)=> a + b;
const resta = (a , b)=> a - b;
```
### index.js
```javascript
console.log('Inicia la ejecucion de mi programa');
console.log('Vamos a hacer una suma');
const resultado = suma(4,5);
console.log(resultado)// esto nos va a devolver 'suma is not defined' por que la funcion suma no esta dentro de 'index.js', sino que esta dentro de 'funciones.js'
```
Para poner a disposicion las funciones de 'funciones.js' utilizamos el metodo .exports de los module, asi exportamos un objeto entero.
*Importante:* Se dice que podenmos a disposicion (no exportamos) para que cualquier modulo que requiera, pueda utilizar las funciones dentro del modulo 'funciones.js'

### funciones.js
```javascript
//    funciones.js

const suma = (a , b)=> a + b;
const resta = (a , b)=> a - b;

module.exports = {
    suma,  // ----> suma = suma;
    resta, // ---->resta = resta;
}
```

Y en el modulo a utilizarlo (en este caso quiero utilizarlo en 'index.js') se hace un 'requiere'
significa que en ese modulo se esta requiriendo lo que 'funciones.js' puso a disposicion  

Ej:
```javascript
//        En index.js

const obj = require('./funciones') // Asi se hace el require
console.log('Inicia la ejecucion de mi programa');
console.log('Vamos a hacer una suma');
//const resultado = suma(4,5);//--->> aca tendria que modificar y hacerlo asi:
const resultado = obj.suma(4, 5); 
console.log(resultado)
```

## Requerir solo una propiedad (funcion)
Si en nuestro 'funciones.js' tenemos muchas funciones, y solo necesitamos utilizar o requerir solo una funcion
Ej:
```javascript
//     En funciones.js

module.exports = {
    suma,
    resta,
    division,
    multiplicacion,
    potencia
}
```
Lo que se hace en el modulo que se requiere (en este caso en el 'index.js') es hacer el metodo require solo de esa funcion, para eso utilizamos destructuracion del objeto 'require'

Ej:
```javascript
//    En index.js

const {suma} = require ('./funciones');  //Esto trae o manda a requerir solo la funcion 'suma'
```

# 2_ Metodo export - import (ES6)
Este metodo lo vamos a usar para el front-end

## En index.js
Teniendo funciones en el modulo 'funciones.js' 

Ej:

```javascript
//      funciones.js

const suma = (a, b)=> a+b;

const resta = (a , b)=> a - b;

const multiplicacion = (a, b) => a * b;

const division = (a, b)  => a / b;

```

- Para exportar suma y resta se utiliza la palabra reservada 'export'

```javascript
//      funciones.js

export const suma = (a, b)=> a+b;

export const resta = (a , b)=> a - b;

const multiplicacion = (a, b) => a * b;

const division = (a, b)  => a / b;

```
Tambien se puede hacer


```javascript
//      funciones.js

export const suma = (a, b)=> a+b;

export const resta = (a , b)=> a - b;

const multiplicacion = (a, b) => a * b;

const division = (a, b)  => a / b;

```

## Y en el modulo index.js
```javascript
//      index.js

import {suma} from './funciones'
import {num1, num2} from './variables' // para importar variables de por ej 'variables.js'
```
# WEBPACK

Webpack lo que va a hacer es fijarse que dependencias tiene mi archivo index.js, y los reune todos en un solo modulo
Entonces nosotros trabajamos de forma ordenada, con modulos organizados.
Webpack arma un unico archivo js donde estan todos esos modulos (hace un bundle)
*bundle es el archivo que va a leer el navegador*  
  


![img](/img%20y%20screenshot/05_Bundlers.jpg)

---

## Como usar WEBPACK en nuestro proyecto

![img](/img%20y%20screenshot/05_Bundlers(2).jpg)

## 1_Instalar webpack webpack-cli
```javascript
//      En consola
npm install webpack webpack-cli
```

## 2_ Ir a package.json y escribir la propiedad build:

Agregar al objeto 'scripts' que está dentro del package.json las propiedades 'start' y 'build':

```javascript
//      En package.json
"scripts": {
    "start": "node server.js"; // (parece que no es necesario) 
    "build": "webpack" // Este si
}
``` 


## 3_ Crear archivo webpack.config.js en nuestro proyecto:

Crear un archivo 'webpack.config.js', en este arhivo vamos a insertar un objeto (module.exports) que contiene 2 propiedades: 'entry' y 'output' con los siguientes valores:

```javascript
//      En webpack.conig.js (que creamos)
module.exports = {
    entry: './index.js',  // en entrada vamos a indicar el archivo que requiere de 
                          //todos los modulos, pero no exporta nada (index.js)

    output:{              //En output es el modulo bundler donde va a guardar el archivo final
        path: __dirname +'./webpack' // Esto nos va a crear una carpeta 'webpack',__dirname
                                     //usar si o si
        filename: 'bundle.js' // El nombre que le vamos a poner al archivo resultante
    }
}
```
*EL__dirname es el nombre de la carpeta que yo tengo ahora, por eso se usa __dirname + el nombre que nosotros querramos darle*

## 4_Hacer que nuestro navegador encuentre nuestro bundler.
Donde esta el **bundler**  ??

### En consola hacemos correr el webpack:
```
run build
``` 
*Esto crea el output que le dijimos, la carpeta webpack con el archivo adentro 'budnle.js'*  

**-Este archivo 'bundle.js' tiene todo lo que creamos en todos nuestros modulos, ('index.js', 'funciones.js', 'variables.js', etc etc etc)**  

Ahora tenemos todo en un solo archivo, y llamamos ese archivo desde nuestro HTML con un solo script  
Ej:
```html
<!--     En nuestro HTML (index.html)

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title> -->
    <script src = "./webpack/bundle.js"></script>
 <!-- 
</head>
<body>
</body>
</html> -->
```

