#      DOM Avanzado
## Selectors
Los principales 5 selectores son los siguientes:

## 1_ getElementsByClassName
`document.getElementsByClassName` se encarga de encontrar elementos en función del nombre de su clase. Devuelve un array conteniendo los objetos que coincidieron con la búsqueda que puede ser iterado. Debemos brindarle como parámetro un string con el nombre de la clase que deseamos buscar. Ejemplo:
```javascript
const divs = document.getElementsByClassName('divClass');
```
##### *En este ejemplo estamos buscando los elementos que contengan 'divClass' como su clase definida*
---
## 2_ getElementById
`document.getElementById` se encarga de encontrar un único elemento en función de su id, por lo que devolverá dicho elemento. Debemos brindarle como parámetro un string con el id del elemento que deseamos buscar. Ejemplo:
```
const div = document.getElementById('divId');

```
##### *En este ejempo estamos buscando el elemento cuyo id es igual a 'divId'*
---
## 3_ querySelector
`document.querySelector` es un método que busca los elementos basándose en uno o más selectores CSS. Recordemos que es posible hacer referencia a clases utilizando un . a ids con # y a elementos usando el nombre de su etiqueta directamente. Es recomendable utilizar sólo ids con querySelector ya que sólo retornará el primer elemento que coincida con el selector indicado. Ejemplo:
```javascript
 const div = document.querySelector('.divId');
 ```
##### * En este ejemplo obtendremos el primer elemento con la clase 'divId' pero si hay más elementos con dicha clase no los tendrá en cuenta*
---
## 4_ querySelectorAll
`document.querySelectorAll` funciona de la misma forma que querySelector pero en vez de devolver únicamente el primer elemento que coincida con el selector devolverá un array con todos los elementos que coincidan y retorna un arreglo que contiene todos los elementos que coincidan con el selector. Ejemplo:
```javascript
const divs = document.querySelectorAll('.divId');
```
##### *En este caso obtendremos un array con todos los elementos que contencan la calse 'divld'*
---
## 5_ createElement
En el caso de que queramos crear un elemento para agregarlo al DOM podemos utilizar `document.createElement`. Este método recibe como parámetro un string indicando el tipo de elemento que deseamos crear y devuelve un elemento vacío de dicho tipo. Ejemplo:
```javascript
const newDiv = document.createElement('div');
```
##### *En este ejemplo estamos creando un nuevo elemento 'div' vacio.*
---
---
---
# Element Methods
Una vez seleccionado el elemento podemos utilizar distintos métodos y propiedades para modificarlo como por ejemplo cambiar su estilo, cambiar de atributos, agregar/eliminar elementos anidados, agregar/eliminar `event listeners`. Algunos de los métodos más comunes son:
## 1_  .innerHTML
Con el método `innerHTML` podemos acceder a la información que se encuentra entre las etiquetas de apertura y cierre de un elemento HTML tanto para simplemente lectura o para su modificación. Ejemplo:
```javascript
    const p = document.querySelector('#pId');
    console.log(p.innerHtml) // Va a imprimir el texto dentro del párrafo con el id 'pID'

    p.innerHTML = 'Nuevo texto'; // Acá estamos modificando el texto del párrafo mencionado anteriormente

    console.log(p.innerHTML); // Va a imprimir el nuevo texto que le seteamos, es decir: "Nuevo texto"
```
---
## 2_ .[attribute] y .setAttribute

Podemos llamar al método `.setAttribute` para agregar un atributo a un elemento o sobreescribirlo en el caso de que ya se encuentre definido. Otra forma equivalente de realizarlo pero más corta sería llamando a `.[nombre del atributo] = [nuevo valor]`. Ejemplo:

```javascript
    const a = document.querySelector('#linkHenry'); // Obtengo el elemento a cuyo id es 'linkHenry'

    a.setAttribute('href', 'https://www.soyhenry.com/'); // Seteo el atributo href del elemento a para que redireccione a la página principal de Henry

    a.href = 'https://www.soyhenry.com/'; // Equivalente al anterior pero más corto
```
---
## 3_ .style

Podemos modificar el estilo de un elemento utilizando `.style`. Cabe mencionar que con esto no estamos accediendo al estilo CSS sino que lo que estamos haciendo es agregarle la propiedad `style` dentro de la etiqueta HTML. Ejemplo:

```javascript
    const div = document.querySelector('#divId');

    div.style.height = '300px'; // Le damos una altura de 300 pixeles al div cuyo id es 'divId'
    div.style.background = 'red'; // Le seteamos el color de fondo en rojo a dicho div
```
---
## 4_ .className y .id

Podemos utilizar `.className` y `.id` para acceder y modificar las clases o ids de los elementos. Esto es útil cuando ya tenemos definido en los estilos CSS un estilo en particular asociado a una clase o id y queremos simplemente modificando la clase o id del elemento cambiar su estilo sin tener que modificar propiedad por propiedad. Ejemplo:

```javascript
    const div = document.querySelector('#divId');

    console.log(div.id); // Utilizando ',id' accedemos al nombre de su id, en este caso 'divId'
    div.className = 'nuevaClase'; // Le seteamos la clase 'nuevaClase'
    div.id = 'nuevoId'; // Le seteamos el id 'nuevoId'
```
## 5_ .appendChild

Es posible agregar elementos directamente al `DOM` utilizando `.appendChild` sobre el elemento que queremos que sea su padre. Ejemplo:

```javascript
    const body = document.querySelector('body');
    const newDiv = document.createElement('div'); // Creamos un nuevo elemento div

    body.appendChild(newDiv); // Agregarmos el div recién creado dentro del body de la paǵina

```
---
# Event Listeners:

Un `Event Listener` es una función que se ejecuta luego de que ocurra un determinado evento. Existen diferentes tipos de eventos, entre ellos se encuentran: un click, un desplazamiento del mouse por encima del elemento, el apretado de una tecla, etc. Para ver la lista completa pueden consultar el siguiente [link](https://developer.mozilla.org/es/docs/Web/Events)

---
### Click

El evento más común es el de 'click' y en particular es el único que posee la propiedad `.onclick` para asignarle una función que será ejecutada al clickear el componente indicado. Ejemplo:

```javascript
    const div = document.querySelector('#divId');
    div.onclick = function() {
        console.log('clickeado');
    };
```
##### *En este ejemplo lo que estamos haciendo es indicarle que cuando se clickee el div cuyo id es 'divId' se ejecute la función ahí definida que lo único que hará en este caso es escribir por consola "clickeado"*
---       
### addEventListener y otros eventos


`.addEventListener` es un método que recibe como primer parámetro el tipo de evento que va a estar esperando y como segundo parámetro una función callback que es la que va a ejecutarse cuando ocurra dicho evento. Nota: es mejor utilizar addEventListener en todos los casos incluyendo los clicks. Ejemplo:

```javascript
    const div = document.querySelector('#divId');
    div.addEventListener('mouseenter', function() {
        console.log('El mouse entró!');
    });
```
##### *En este ejemplo lo que estamos haciendo es indicarle que cuando el mouse ingrese al div cuyo id es 'divId' se ejecute la función ahí definida que lo único que hará en este caso es escribir por consola "El mouse entró!"*

---
---

# CODE REVIEW :
 
setAttribute()
se le pasa como primer parametro el tipo a crear y el segundo como queremos que se llame el valor