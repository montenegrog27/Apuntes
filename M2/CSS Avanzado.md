# CSS Avanzado 


## CSS Media Queries

Para poder determinar que una propiedad solo se aplique en función del tamaño de la pantalla del dispositivo tenemos la posibilidad de usar `CSS Media Queries`.

Supongamos que queremos modificar el color de fondo de la página web:

* Negro para una pantalla de 600px o menos de ancho
* Azul para una pantalla de entre 600px a 900px de ancho
* Rojo para una pantalla de más de 900px de ancho

```css
body {
  background-color: red;
}

/* Pantallas de menos de 992px de ancho */
@media screen and (max-width: 992px) {
  body {
    background-color: blue;
  }
}

/* Pantallas de menos de 600px de ancho */
@media screen and (max-width: 600px) {
  body {
    background-color: black;
  }
}
```

# LESS
## Mixins

Los mixins nos permiten incluir un set de propiedades ya definido dentro de otro.

```less
.important-text {
  color: black;
  font-size: 25px;
  font-weight: bold;
}
```

Ahí estamos creando el mixin llamado `important-text` que luego podemos utilizar de la siguiente forma:

```less
.danger {
  .important-text();
  background-color: red;
}

.success {
  .important-text();
  background-color: green;
}
```

Esto se va a traducir a codigo CSS quivalente a:

```css
.danger {
  color: red;
  font-size: 25px;
  font-weight: bold;
  border: 1px solid blue;
  background-color: green;
}
```
## Los mixin pueden recibir parámetros:

```less
.bordered(@color; @width) {
  border: @width solid @color;
}

.myArticle {
  .bordered(blue; 1px);// espera que le pasemos un color y un width!
}

// Es posible indicar el nombre del parámetro al invocar el mixin
// para evitar tener que respetar un orden en particular
.myArticle-2 {
  .bordered(@width: 20px; @color: #33acfe);
}
```

*Aquí lo que estamos haciendo es definir un mixin que recibe dos parámetros (color y width) que luego van a ser utilizados para definir el borde del elemento. Con ello podemos reutilizar el mixin simplemente llamándolo con diferentes colores o anchos como en el ejemplo que se le está dando un color azul y un borde de un pixel a los elementos con la clase `myArticle`*

## otro ejemplo:
```css
.buttonbase (@bgcolor; @color; @width; @height; @br){
    background-color:
    color:
    width: 
    height:
    border-radius:
    }
```
Esto es para darle un 