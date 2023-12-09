<!--
    Archivo principal:

    Este archivo principal constituye un formulario interactivo construido mediante el framework Svelte. El formulario incluye diversos campos de entrada, selectores y botones para recopilar información del usuario. Además, se establece una conexión WebSocket para enviar los datos del formulario a un servidor remoto.

    Estructura del formulario:
    - Campos de entrada para Nombre, Apellidos, DNI, Ciudad, Email, Dirección, Teléfono y Matrícula.
    - Etiquetas y campos de entrada con tipo "date" para Fecha de Entrada, Fecha de Nacimiento y Fecha de Expedición.
    - Un selector con el nombre "parcela".
    - Un botón de luz.
    - Un botón de envío para procesar y enviar el formulario.

    Conexión WebSocket:
    - Se establece una conexión WebSocket con un servidor en la dirección 'ws://192.168.1.96:9500/' al cargar la página.
    - Se manejan eventos de apertura y cierre de la conexión para informar al usuario sobre el estado de la conexión.

    Envío de formulario:
    - Al enviar el formulario, se recopilan los datos de los campos y se almacenan en el objeto formData.
    - Se verifica si se ha seleccionado una parcela antes de enviar los datos.
    - Se muestra una alerta indicando si el formulario fue enviado correctamente.
    - Los datos del formulario se envían al servidor a través de la conexión WebSocket.

    Estilos:
    - Se aplica un estilo mínimo al formulario, con un espacio superior de 20px.
    - Se ajusta el tamaño de fuente de las etiquetas para mejorar la legibilidad.

    Nota: Este código está diseñado para ser utilizado por alguien que no haya desarrollado nada del mismo. Se espera que el usuario modifique o amplíe el formulario según sus necesidades.
-->

<script>
    // Importación de componentes Svelte y del entorno de navegador
    import Inputs from "./Inputs.svelte";
    import Selector from "./selectorParcelas.svelte";
    import Boton_luz from "./boton_luz.svelte";
    import { browser } from "$app/environment";
    import Acompanante from "./Acompanante.svelte";
    import { afterUpdate } from 'svelte';

    let mostrarAcompanante = false;

    // Inicialización de variables y conexión WebSocket
    let socket;
    let isConnected = false;

    if (browser) {
        // Establecimiento de la conexión WebSocket al cargar la página
        socket = new WebSocket('ws://10.182.122.193:9500/');

        // Manejo del evento de cierre de la conexión
        socket.onclose = function () {
            isConnected = false;
            console.log("Desconectado del servidor WebSocket");
            alert("No se puede conectar con el servidor, recargue la página");
        }

        // Manejo del evento de apertura de la conexión
        socket.onopen = function () {
            isConnected = true;
            console.log("Conectado al servidor WebSocket");
        }
    }

    // Función para comprobar si se ha seleccionado clientes
    function Comprobacion() {
        return document.getElementById('clientes').value !== '-';
    }

    afterUpdate(() => {
        mostrarAcompanante = Comprobacion();
    });

    // Objeto para almacenar datos del formulario
    let formData = {};

    // Función para enviar el formulario
    function enviarFormulario() {
        // Verificación de la selección de parcela antes de enviar los datos
        if (document.getElementById('parcela').value !== '-') {
            // Recopilación de datos de los campos del formulario
            let NumAcompanante = document.getElementById('clientes');
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
                    luz: document.getElementById('Luz').checked,
                    Ncliente: document.getElementById('clientes').value
                }
            };
            if (NumAcompanante.value > 0) {
                for (let i = 0; i < NumAcompanante.value; i++) {
                    formData["Acompanante: " + i] = {
                        nombre: document.getElementById('Nombre' + i).value,
                        apellidos: document.getElementById('Apellidos' + i).value,
                        dni: document.getElementById('DNI' + i).value,
                        tipo_documento: document.getElementById('Documento' + i).value,
                        sexo: document.getElementById('Sexo' + i).value
                    };
                }
            }
            // Muestra una alerta indicando que el formulario ha sido enviado.
            alert("Formulario enviado");
            // Registra en la consola un mensaje indicando que el formulario ha sido enviado.
            console.log(formData);
            // Envío de los datos del formulario al servidor a través de la conexión WebSocket
            socket.send(JSON.stringify(formData));
        } else {
            // Alerta si no se ha seleccionado una parcela
            alert("Datos no enviados, no ha seleccionado parcela");
        }
    }
</script>

<body>
<!-- Contenedor principal del formulario -->
<div class="main">
    <!-- Formulario con campos de entrada, selectores y botones -->
    <form on:submit={enviarFormulario}>

        <!-- Campos de Entrada -->
        <Inputs name="Nombre" id="Nombre" type="text" />
        <Inputs name="Apellidos" id="Apellidos" type="text" />
        <Inputs name="DNI" id="DNI" type="text" />
        <Inputs name="Ciudad" id="Ciudad" type="text" />
        <Inputs name="Email" id="Email" type="text" />
        <Inputs name="Dirección" id="Direccion" type="text" />
        <Inputs name="Telefono" id="Telefono" type="text" />
        <Inputs name="Matricula" id="Matricula" type="text" />

        <!-- Campos de Fecha -->
        <label for="fecha_Entrada">Fecha entrada <Inputs name="fecha Entrada" id="fecha_Entrada" type="date" /></label>
        <label for="fecha_Nacimiento">Fecha nacimiento <Inputs name="fecha Nacimiento" id="fecha_Nacimiento" type="date" requerido=false /></label>
        <label for="fecha_Expedicion">Fecha expedición <Inputs name="fecha Expedicion" id="fecha_Expedicion" type="date" /></label>

        <!-- Contenedor para Selector, Botón de Luz y Componente de Envío -->
        <div id="con">
            <Selector name="parcela" />
            <Selector name="clientes" />
            <Boton_luz />
        </div>

        <!-- Llama al componente Acompañante si Comprobacion es true   -->
        {#if mostrarAcompanante}
        <Acompanante />
        {/if}

        <!-- Botón de envío del formulario -->
        <Inputs name="boton" id="boton" type="submit" />
    </form>
</div>
</body>



<style>
    /* Estilos generales para el formulario principal */
    .main {
        padding-top: 20px;
    }



    /* Ajuste de tamaño de fuente para mejorar la legibilidad de las etiquetas */
    label {
        font-size: 12px;
    }
</style>


