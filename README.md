
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/css/bootstrap.min.css"
        integrity="sha384-B0vP5xmATw1+K9KRQjQERJvTumQW0nPEzvF6L/Z6nronJ3oUOFUFpCjEUQouq2+l" crossorigin="anonymous">
    <link rel="stylesheet" href="index.css">
    <title>Document</title>
    
    <style>form {
        margin-top: 1rem;
        margin-bottom: 1rem;
    }
    
    .container {
        
        margin-top: 20px;
        margin-left: auto;
        margin-right: auto;
        padding-left: 20px;
        padding-right: 20px;
        width: 100%;
    }
    
    .sexy {
        column-fill: balance;
        flex-wrap: wrap;
        align-content: center;
    }

   

    
    </style>
</head>

<body>
    <script>"use strict";

        //Creamos un objeto llamado Producto, con sus propiedades
        //Utilizando el patrón de diseño Prototype
        class Producto {
            constructor(nombre, valor, cantidad) {
                this.nombre = nombre;
                this.valor = valor;
                this.cantidad = cantidad;
            }//Permite convertir el objeto a texto legible
            toString() {
                return `Nombre: ${this.nombre}, Valor: ${this.valor}, Cantidad: ${this.cantidad}, Total: ${this.valor * this.cantidad}`;
            }
        }
        //Creamos un objeto Inventario donde productos es un arreglo
        class Inventario {
            constructor(listaProductos) {
                this.productos = listaProductos;
            }
            //Con este método agrego nuevos productos al arreglo productos
            agregar(productoNuevo) {
                //TODO Una manera de usar 'Spread': this.productos = [...this.productos, ...[productoNuevo]];
                //TODO para crear un nuevo arreglo usando un arreglo existente como parte de él
                this.productos.push(productoNuevo);
            }
        }
        //Creamos un objeto inventarioRopa y asigno un arreglo vacío
        //Se pueden crear otros objetos Inventarios para otras categorías
        let inventarioRopa = new Inventario([]);
        
        //Esta función permite agregar productos al arreglo a través de los input del HTML
        function ingresar() {
            let nombre = document.getElementById("nombre").value;
            let valor = Number(document.getElementById("valor").value);
            let cantidad = Number(document.getElementById("cantidad").value);
            document.getElementById("correcto").innerText = '';
        
            // Función flecha para validar todos los campos
            //Devuelve el mismo mensaje en caso que el valor no sea numérico para 'valor' y 'cantidad'
            let validar = (() => {
                //Verificación de campos vacíos
                let mensaje = "";
        
                if (nombre == "") {
                    mensaje += "Ingrese un nombre" + '\n';
                }
                if (valor == "") {
                    mensaje += "Ingrese un valor" + '\n';
        
                }
                if (cantidad == "") {
                    mensaje += "Ingrese una cantidad" + '\n';
                }
                //Verificación de valores numéricos
                if (isNaN(valor)) {
                    mensaje += "Ingrese un valor" + '\n';
                }
                if (isNaN(cantidad)) {
                    mensaje += "Ingrese una cantidad" + '\n';
                }
                let parrafo_errores = document.getElementById("mensaje");
                parrafo_errores.innerText = mensaje;
                //Si no hay mensajes de error, retorna true
                return mensaje == "" ? true : false;
            })
        
            //Si la validación esta ok y retorna true, se agrega el producto al inventario
            //Si la validación retorna false, el producto no se agrega
            if (validar()) {
        
                let nuevo = new Producto(nombre, valor, cantidad);
                inventarioRopa.agregar(nuevo);
                document.getElementById("correcto").innerText = `Producto agregado correctamente`;
                document.getElementById("formulario").reset();
            }
        }
        
        function listar() {
            let resultado = document.getElementById("lista");
            //!Primer intento (los resultados me quedaban separados por comas)
            // resultado.innerText = inventarioRopa.productos.toString();
            // console.log(inventarioRopa.productos.toString());
        
            if (inventarioRopa.productos == "") { //si se aprieta listar sin haber ingresado productos
                resultado.innerText = "No ha ingresado ningún producto aún";
            } else {
                //!solución: usar un forEach() que ejecuta la función indicada una vez por cada elemento del array.
                document.getElementById("lista").innerText = ""; // vaciar lista
                inventarioRopa.productos.forEach(productos => resultado.innerText += productos.toString() + '\n');
                inventarioRopa.productos.forEach(productos => console.log(productos.toString()));
            }
        }
        
        </script>

    <div class="container">

        <div class="w-70 p-3 border border-warning rounded p-3 mb-2 bg-light">
            <h3>Ingreso de Productos</h3>
            <form action="" onsubmit="return false;" id="formulario">
                <label for="">Nombre:</label><br>
                <input type="text" id="nombre"><br>
                <label for="">Valor:</label><br>
                <input type="text" id="valor"><br>
                <label for="">Cantidad:</label><br>
                <input type="text" id="cantidad"><br>
                <br>
                <button onclick="ingresar()" class="btn btn-primary">Ingresar</button>
            </form>
            <div id="mensaje" class="text-danger"></div>
            <p id="correcto" class="text-success"></p>
            <hr>

            <button onclick="listar()" class="btn btn-success">Listar Productos</button>
            <br><br>
            <div class="okis">
            <h3>Lista de productos</h3>
            <div class="sexy"><p id="lista"></p></div>
            </div>
                
        </div>

    </div>
    


    <script src="index.js"></script>
</body>

</html>
