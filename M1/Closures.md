# Closures
``` javascript
function saludar (saludo) {
    return function (nombre) {
        console.log(saludo + ' ' + nombre)
    }
}
var saludarHola = saludar('Hola')
saludar('toni') // Hola Toni
```


