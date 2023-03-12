# AJAX

HTTP Es un protocolo de comunicacion del cliente con el servidor

### Metodos HTTP para pedir al servidor con AJAX:
 
####   - Post: Para guardar informacion
####   - Get: Peticion de informacion
####   - Delete: Eliminar una informacion
####   - Put : Para que modifique



![img](/img%20y%20screenshot/Ajax%20img2.jpeg)
### *Importante: El servidor siempre va a devolver una respuesta, aun cuando no pueda hacer lo que le estamos pidiendo*

---

## Como usar AJAX
Primero en nuestro html en el head insertamos el script de la pag de jquery
```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
```

---

## Como seleccionar un id para trabajar con jquery:
por ejemplo, en HTML tenemos un div con un id = 'amigos'
entonces seleccionamos ese div con la siguiente sintaxis
```
$('#amigos').
```
## Metodo .click():
el metodo click lo que hace es un eventListener al hacer click, recibe como parametro una callback, que es lo que va a hacer cuando se realice el click
```
$('#amigos').click()
```
## Metodo .val():
El metodo .val() lo que hace es traer el valor de lo que le estamos aplicando el metodo

---


# Metodo Get: Peticion de informacion
### Como crear una solicitud GET:

1_ Dentro de un script en HTML en el body
   escribimos:
   ```HTML
   $
   ```  
   --->> Este signo de pesos representa a la libreria jQuery


2_ primero se le pasa un parametro que es la url del servidor que le quiero hacer la request:

```javascript
   $.get("https://jsonplaceholder.typicode.com/users")
```
3_ El segundo parametro que le enviamos a get es una funcion callback(la respuesta):

   ```javascript
   $.get("https://jsonplaceholder.typicode.com/users"(response)=>{

   })
   ```
   Esta callback se va a ejecutar cuando se ejecute el primer parametro. En este caso un console.log:

   ```javascript
   $.get("https://jsonplaceholder.typicode.com/users"(response)=>{
    console.log(response);
   })
   ```

---


# Metodo Delete: Eliminar una informacion
Para eliminar una informacion vamos a uar la siguiente sintaxis:
```javascript
$.ajax({
    url: ""// Aca va la url
    type "DELETE" // aca va DELETE
    success: ()=> {}// Esta es la callback de que hacemos cuando termina
})
```
*Importante*: Todos los metodos (GET, DELETE, PUT y POST) usan la misma sintaxis, solo que al metodo GET se puede usar la sintaxis abreviada (Solo a ese metodo)



