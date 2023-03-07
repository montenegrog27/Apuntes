# AJAX

HTTP Es un protocolo de comunicacion del cliente con el servidor

Metodos HTTP para pedir al servidor con AJAX:
 
## Post: Para guardar informacion
## Get: Peticion de informacion
## Delete: Eliminar una informacion
## Put : Para que modifique

![img](/img%20y%20screenshot/Ajax%20img2.jpeg)
### *Importante: El servidor siempre va a devolver una respuesta, aun cuando no pueda hacer lo que le estamos pidiendo*

### Como usar AJAX
Primero en nuestro html en el head
```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
```
## Metodo Get: Peticion de informacion
### Como crear una solicitud GET:

1_ Dentro de un script en HTML en el body
   escribimos 
   ```HTML
   $
   ```  
   --->> Este signo de pesos representa a la libreria jQuery


2_ primero se le pasa un parametro que es la url del servidor que le quiero hacer la request

```javascript
   $.get("https://jsonplaceholder.typicode.com/users")
```
3_ El segundo parametro que le enviamos a get es una funcion callback(la respuesta)

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



## Metodo Post: Para guardar informacion
### Como crear una solicitud POST:




## Delete: Eliminar una informacion
```javascript
$.ajax({
    url: ""// Aca va la url
    type "DELETE" // aca va DELETE
    success: ()=> {}// Esta es la callback de que hacemos cuando termina
})
```

## Put : Para que modifique

