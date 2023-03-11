# BUNDLERS
## Modulos:

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
module.exports = {
    suma,
    resta,
    division,
    multiplicacion,
    potencia
}
```
Lo que se hace en el modulo que se requiere (en este caso en el 'index.js') es hacer el metodo require solo de esa funcion
        
Ej:
```javascript
const {suma} = require ('./funciones');  //Esto trae o manda a requerir solo la funcion 'suma'
```