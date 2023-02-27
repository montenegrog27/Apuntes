# Lo mas importante del M1
## Clase con Mary 27/02
### 1. Que es bracket notation y dot notation?. A que tipos de objetos se les puede aplicar?

- Existen dos formas de acceder a un elemento en arreglos y objetos:

    * dot notation: Se escribe el nombre del objeto seguido de un punto y luego el nombre de la propiedad que queremos acceder Ej:


    * bracket notation: Se escribe la propiedad a la que queremos acceder dentro de corchetes. Se usa para acceder a una variable que no sabemos cual es el nombre, pero que existe. Tambien te permite acceder a una propiedad que tiene caracteres especiales. Ej:

``` javascript
 let obj = {“foo.Bar”: 2}
  obj[“foo.Bar”] // valid syntax
  obj.foo.Bar //invalid syntax
```


---

### 2. Que es un array?
- Un array es una coleccion de elementos de datos alamacenados en la memoria, es una escructura donde cada elemento puede ser accedido directamente usando su index number
---
### 3. Que es un objeto?
- Un objeto es un tipo de dato que puede incluir una coleccion de key-value
---
### 4. Se dice que todo en javascript es un objeto… por que?
- Por que todo es un metodo creado en el prototipo de un objeto global. siempre accedemos al metodo o propiedad de la propiedad de un objeto
---
### 5. Como se le llama al contenido dentro de un array? pista: el array puede estar vacio o puede tener uno o mas de ello.
- indice? 
---
### 6. Que es el indice/index para un array?
- El indice es el lugar donde esta posicionado el elemento, un array empieza en el indice 0
---
### 7. Como puedes acceder al elemento de un array?
- See puede acceder mediante dot notation, o mediante corchetes
---
### 8. Menciona al menos 3 maneras/metodos para recorrer un array
- for
- while
- forEach
---
### 9. Los arrays se pueden anidar entre ellos mismos? es decir, podria tener un array dentro de un array mas grande, y dicho array a su vez estar dentro de otro array padre? Si, no, por que?
- Si, un array puede contener cualquier tipo de dato, (array, obj, string, numb, boolean.) y puede tener tambien arrays dentro de array
---
### 10. Como se le llama al contenido dentro de un objeto? pista: “pares”

       Key-Value

- Propiedad: key
- Valor : Value


---
### 11. Como puedes acceder al valor de una key de un objeto? Hay una unica manera de acceder o depende de algo mas?

    - dot notation 
    - bracket notation
---
### 12. Los objetos se pueden anidar entre ellos mismos? es decir, puedo tener un objeto padre que dentro tenga otro objeto y a su vez dicho objeto tenga otro objeto dentro?
- Si, los objetos pueden contener objetos dentro de ellos
---
### 13. Se pueden anidar arrays con objetos? Ya sea arrays que tengan objetos dentro, y/u objetos que tengan dentro a arrays?
- 
# ?
---
###  14. Dado el siguiente objeto de javascript, escriba la posible manera de acceder al valor de la key “developer”:
- objeto[key] 
# ?
