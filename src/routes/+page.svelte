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
    - Se establece una conexión WebSocket con un servidor en la dirección 'ws://10.182.122.193:9500/' al cargar la página.
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

    // Crea una variable reactiva para almacenar el valor del store
    let numAcompanantesValue = 0;

    // Inicialización de variables y conexión WebSocket
    let socket;
    let isConnected = true;  // !!!!!!!!!!!!!!!ESTO HAY QUE CAMBIARLO , PARA LA PRUEBA DEL DIA 13 ESTÁ BIEN ASI

    if (browser) {
        // Establecimiento de la conexión WebSocket al cargar la página
        socket = new WebSocket('ws://localhost:5173/');

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

    // Función para agregar un acompañante
    function agregarAcompanante() {
        numAcompanantesValue += 1;
        // console.log(numAcompanantesValue + " fuera")
    }

    // Función para eliminar un acompañante
    function eliminarAcompanante() {
        // Verifica si hay acompañantes antes de mostrar el mensaje de confirmación
        if (numAcompanantesValue > 0) {
            const confirmacion = window.confirm("¿Estás seguro de eliminar el acompañante?");

            if (confirmacion && numAcompanantesValue > 0) {
                numAcompanantesValue -= 1;
            }
        }
    }

    // Objeto para almacenar datos del formulario

    // Función para enviar el formulario
    async function enviarFormulario() {
        // Verifica si hay conexión antes de intentar enviar los datos
        if (isConnected) {
            // Intenta reconectar al servidor WebSocket
            let intentos = 0;
            const maxIntentos = 3;

            while (!isConnected && intentos < maxIntentos) {
                try {
                    // Intenta abrir la conexión WebSocket
                    await new Promise(resolve => setTimeout(resolve, 1000)); // Espera 1 segundo antes de intentar la reconexión
                    socket = new WebSocket('ws://localhost:5173/');
                    intentos++;

                    // Espera a que la conexión se abra
                    await new Promise((resolve, reject) => {
                        socket.addEventListener('open', resolve);
                        socket.addEventListener('error', reject);
                    });

                    isConnected = true;
                    console.log("Conectado al servidor WebSocket después de reconexión");
                } catch (error) {
                    console.error("Error al intentar reconectar:", error);
                }
            }

            // Si después de los intentos no se logra la conexión, muestra un aviso
            if (!isConnected) {
                alert("No se pudo establecer conexión con el servidor después de varios intentos. Inténtelo de nuevo más tarde.");
                return;
            }

            // Recopilación de datos de los campos del formulario
            if (document.getElementById('parcela').value !== '-') {
                let formData = {};
                let NumAcompanante = numAcompanantesValue
                formData = {
                    cliente: {
                        nombre: document.getElementById('Nombre').value,
                        apellidos: document.getElementById('Apellidos').value,
                        sexo: document.getElementById('sexo').value,
                        tipo_documento: document.getElementById('Documento').value,
                        dni: document.getElementById('DNI').value,
                        ciudad: document.getElementById('Ciudad').value,
                        email: document.getElementById('Email').value,
                        direccion: document.getElementById('Direccion').value,
                        telefono: document.getElementById('Telefono').value,
                        tipo_vehiculo: document.getElementById('vehiculo').value,
                        matricula: document.getElementById('Matricula').value,
                        fechaEntrada: document.getElementById('fecha_Entrada').value,
                        fechaNacimiento: document.getElementById('fecha_Nacimiento').value,
                        fechaExpedicion: document.getElementById('fecha_Expedicion').value,
                        parcela: document.getElementById('parcela').value,
                        luz: document.getElementById('Luz').checked,
                        pais: document.getElementById('Pais').value,
                        Ncliente: NumAcompanante
                    }
                };
                if (NumAcompanante > 0) {
                    for (let i = 1; i <= NumAcompanante; i++) {
                        formData["Acompanante" + i] = {
                            nombre: document.getElementById(`Nombre`+i ).value,
                            apellidos: document.getElementById('Apellidos'+i).value,
                            dni: document.getElementById('DNI' + i).value,
                            tipo_documento: document.getElementById('Documento' + i).value,
                            sexo: document.getElementById('Sexo' + i).value,
                            fechaNacimiento: document.getElementById('fecha_Nacimiento' + i).value
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
                alert("No ha seleccionado parcela");
                return;
            }

        } else {
            alert("No hay conexión al servidor. Inténtelo de nuevo más tarde.");
            return;
        }
    }

</script>


<body>
    <!-- Contenedor principal del formulario -->
    <div class="main">
        <!-- Formulario con campos de entrada, selectores y botones -->
        <form on:submit={enviarFormulario}>
            <h2>Cliente principal</h2>

            <div id="column">
                <!-- Campos de Entrada -->
                <label for="Nombre">Nombre:</label>
                <label for="Apellidos">Apellidos:</label>
                <Inputs name="Nombre" id="Nombre" type="text" />
                <Inputs name="Apellidos" id="Apellidos" type="text" />

                <!-- Selector para el campo 'sexo' -->
                <div>
                    <label for={`sexo`}>Sexo</label>
                    <select id={`sexo`}>
                        <option value="Masculino">Masculino</option>
                        <option value="Femenino">Femenino</option>
                    </select>
                </div>

                <!-- Selector para el campo 'Documento' -->
                <div>
                    <label for="Documento">Documento</label>
                    <select id="Documento">
                        <option value="DNI">DNI</option>
                        <option value="Pasaporte">Pasaporte</option>
                    </select>
                </div>

                <!-- Campos con información general -->
                <label for="DNI">DNI:</label>
                <label for="Ciudad">Ciudad:</label>
                <Inputs name="DNI" id="DNI" type="text" />
                <Inputs name="Ciudad" id="Ciudad" type="text" />
                <label for="Pais">País:</label>
                <label for="Email">Email:</label>
                <Inputs name="Pais" id="Pais" type="text" />
                <Inputs name="Email" id="Email" type="text" />
                <label for="Direccion">Dirección:</label>
                <label for="Telefono">Teléfono:</label>
                <Inputs name="Dirección" id="Direccion" type="text" />
                <Inputs name="Telefono" id="Telefono" type="text" />

                <label for="vehiculo">Tipo vehículo</label>
                <label for="Matricula">Matrícula:</label>
                <select id="vehiculo">
                    <option value="Autocaravana">Autocaravana</option>
                    <option value="Caravana">Caravana</option>
                    <option value="Camper">Camper</option>
                </select>
                <Inputs name="Matricula" id="Matricula" type="text" />

                <!-- Campos de Fecha -->
                <label for="fecha_Entrada">Fecha entrada</label>
                <label for="fecha_Nacimiento">Fecha nacimiento</label>
                <Inputs name="fecha Entrada" id="fecha_Entrada" type="date" />
                <Inputs name="fecha Nacimiento" id="fecha_Nacimiento"  type="date" />
                <div>
                    <label for="fecha_Expedicion">Fecha expedición </label>
                    <Inputs name="fecha Expedicion" id="fecha_Expedicion" type="date"/>
                </div>
                <Selector name="parcela"/>

                <!-- Contenedor para Selector, Botón de Luz y Componente de Envío -->
                <Boton_luz />

            </div>

            <div style="padding-bottom: 22px"></div>
            <!-- Separa el boton de luz de los acompañantes -->
            <Acompanante numAcompanantes={numAcompanantesValue} />

            <!-- Botón para agregar acompañante -->
            <button id="agregar" type="button" on:click={agregarAcompanante}
                >Agregar Acompañante</button
            >

            <!-- Botón para eliminar acompañante, solo si hay acompañantes -->
            {#if numAcompanantesValue > 0}
                <button
                    id="eliminar"
                    type="button"
                    on:click={eliminarAcompanante}>Eliminar Acompañante</button
                >
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

    #column {
        display: grid;
        grid-template-columns: 1fr 1fr;
    }

    /* Ajuste de tamaño de fuente para mejorar la legibilidad de las etiquetas */
    label {
        margin-right: 4px;
        margin-left: 13%;
        font-size: 12px;
        font-family: Helvetica, sans-serif;
        font-weight: bold;
        display: inline;
    }

    h2 {
        padding-bottom: 25px;
        margin-left: 20px;
        font-family: Helvetica, sans-serif;
        font-weight: bold;
    }

    button {
        display: flex;
        justify-content: center;
        align-items: center;
    }

    #row{
        display: grid;
        grid-template-rows: 1fr 1fr;
    }

    #agregar,
    #eliminar {
        padding: 12px 20px;
        font-size: 18px;
        display: inline-block;
        width: 218px;
        cursor: pointer;
        transition: background-color 0.3s ease, border-color 0.3s ease, color 0.3s ease;
        margin-bottom: 10px; /* Ajusta según sea necesario */
        border-radius: 50px;
        color: white;
    }

    #agregar {
        background-color: #4CAF50;
        border: 2px solid #000000;
        margin-left: 50%; /* Centra el botón "Agregar Acompañante" */
        transform: translateX(-50%); /* Centra el botón correctamente */
    }

    #eliminar {
        background-color: #e74c3c;
        border: 2px solid #000000;
        margin-left: 50%; /* Centra el botón "Eliminar Acompañante" */
        transform: translateX(-50%); /* Centra el botón correctamente */
    }

    /* Estilo para el select */
    select {
        padding: 5px;
        border: 1px solid #000000;
        border-radius: 4px;
        cursor: pointer;
        font-size: 12px;
        font-family: Helvetica, sans-serif;
        margin-bottom: 10px;
    }
    /* Estilo para el select de vehículo */
    #vehiculo {
        padding: 5px;
        border: 1px solid #000000;
        border-radius: 4px;
        cursor: pointer;
        font-size: 12px;
        font-family: Helvetica, sans-serif;
        margin: 10px 0 10px 11% ;
        width: 150px; /* Puedes ajustar el valor según tus necesidades */
        height: 25px; /* Puedes ajustar el valor según tus necesidades */
    }





</style>
