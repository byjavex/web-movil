    <!--
        Archivo principal:

        Este archivo principal importa varios componentes para construir un formulario.
        Incluye campos de entrada, selectores, un botón de luz y un componente para el envío del formulario.

        Estructura del formulario:
        - Campos de entrada para Nombre, Apellidos, DNI, Ciudad, Email, Dirección, Teléfono y Matrícula.
        - Etiquetas y campos de entrada con tipo "date" para Fecha de Entrada, Fecha de Nacimiento y Fecha de Expedición.
        - Un selector con el nombre "parcela".
        - Un botón de luz.
        - Un componente para el envío del formulario.

        Estilo:
        - Se aplica un estilo mínimo para el diseño general, con un espacio superior de 20px.
    -->

    <script>
        import Inputs from "./Inputs.svelte";
        import Selector from "./selectorParcelas.svelte"
        import Boton_luz from "./boton_luz.svelte"
        import {browser} from "$app/environment";

        let socket;
        let isConnected = false;

        if (browser) {
            socket = new WebSocket('ws://192.168.1.96:9500/');

            socket.onclose = function () {
                isConnected = false;
                console.log("Desconectado del servidor WebSocket");
                alert("No se puede conectar con el servidor, recargue la pagina")
            }

            socket.onopen = function () {
                isConnected = true;
                console.log("Conectado al servidor WebSocket");
            }


        }
        let formData = {};
        function enviarFormulario() {

            if (document.getElementById('parcela').value !=='-') {
                formData = {
                    cliente: {
                        nombre: document.getElementById('Nombre').value,
                        apellidos: document.getElementById('Apellidos').value,
                        dni: document.getElementById('DNI').value,
                        ciudad: document.getElementById('Ciudad').value,
                        email: document.getElementById('Email').value,
                        direccion: document.getElementById('Direccion').value,
                        telefono: document.getElementById('Telefono').value,
                        matricula: document.getElementById('Matricula').value,
                        fechaEntrada: document.getElementById('fecha_Entrada').value,
                        fechaNacimiento: document.getElementById('fecha_Nacimiento').value,
                        fechaExpedicion: document.getElementById('fecha_Expedicion').value,
                        parcela: document.getElementById('parcela').value,
                        luz: document.getElementById('Luz').checked
                    },
                };
                // Muestra una alerta indicando que el formulario ha sido enviado.
                alert("Formulario enviado");
                // Registra en la consola un mensaje indicando que el formulario ha sido enviado.
                console.log(formData);
                socket.send(JSON.stringify(formData));

            } else{
                alert("Datos no enviados, no ha seleccionado parcela")
            }


        }

    </script>

<body>
<div class="main">
    <form on:submit={enviarFormulario}>
        <!-- Campos de Entrada -->
        <Inputs name="Nombre" id="Nombre" type="text"/>
        <Inputs name="Apellidos" id="Apellidos" type="text"/>
        <Inputs name="DNI" id="DNI" type="text"/>
        <Inputs name="Ciudad" id="Ciudad" type="text"/>
        <Inputs name="Email" id="Email" type="text"/>
        <Inputs name="Dirección" id="Direccion" type="text"/>
        <Inputs name="Telefono" id="Telefono" type="text"/>
        <Inputs name="Matricula" id="Matricula" type="text"/>

        <!-- Campos de Fecha -->
        <label for="fecha_Entrada">Fecha entrada     <Inputs name="fecha Entrada" id="fecha_Entrada" type="date"/></label>
        <label for="fecha_Nacimiento">Fecha nacimiento   <Inputs name="fecha Nacimiento" id="fecha_Nacimiento" type="date" requerido=false /></label>
        <label  for="fecha_Expedicion">Fecha expedición   <Inputs name="fecha Expedicion" id="fecha_Expedicion" type="date"/></label>




        <!-- Selector, Botón de Luz y Componente de Envío -->
    <Selector name="parcela"/>
    <Boton_luz/>
        <Inputs name="boton" id="boton" type="submit"/>
    </form>
</div>
</body>

<style>
    /* Estilos generales para el formulario principal */
    .main {
        padding-top: 20px;
    }

    label{
        font-size: 12px;

    }
</style>


