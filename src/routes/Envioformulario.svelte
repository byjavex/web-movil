<!--
    Botón de Confirmación de Reserva:

    Este componente define un botón que, al hacer clic, muestra una alerta y registra en la consola que el formulario ha sido enviado.

    Estructura:
    - Una función (`enviarFormulario`) que se llama al hacer clic en el botón. Esta función muestra una alerta y registra un mensaje en la consola.
    - Un botón que llama a la función `enviarFormulario` cuando se hace clic.

    Estilos:
    - Se aplican estilos para dar formato al botón, incluyendo tamaño, color de fondo, color de texto, bordes redondeados y una transición suave para el cambio de color de fondo.
-->

<script>
    // Función para manejar el clic en el botón.
    function enviarFormulario() {
        // Muestra una alerta indicando que el formulario ha sido enviado.
        alert("Formulario enviado");

        // Registra en la consola un mensaje indicando que el formulario ha sido enviado.
        console.log("Enviado");
    }
</script>

<!-- Botón de Confirmación de Reserva -->
<button on:click={enviarFormulario}>Confirmar Reserva</button>

<style>
    /* Estilos para el botón */
    button {
        padding: 10px 20px;
        font-size: 16px;
        background-color: #5bcc26; /* Color de fondo */
        color: #000000; /* Color de texto */
        border: black; /* Sin borde */
        border-radius: 30px; /* Bordes redondeados */
        transition: background-color 0.3s ease; /* Transición para suavizar el cambio de color de fondo */
        display: block; /* Hace que el botón sea un bloque para poder aplicar márgenes automáticos */
        margin: 10px auto; /* Centra el botón horizontalmente */
    }
</style>
