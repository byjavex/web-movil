<script>
    function enviarFormulario() {
        alert("Formulario enviado");
        console.log("Enviado");
    }
</script>


<button on:click={enviarFormulario}>Confirmar Reserva</button>
<style>
    button {
        padding: 10px 20px;

        font-size: 16px;
        background-color: #5bcc26; /* Color de fondo */
        color: #000000; /* Color de texto */
        border: black; /* Sin borde */
        border-radius: 30px; /* Bordes redondeados */
        transition: background-color 0.3s ease; /* Transición para suavizar el cambio de color de fondo */
        display: block; /* Hace que el botón sea un bloque para poder aplicar márgenes automáticos */
        /* Centra el botón horizontalmente */
        margin: 10px auto ;
    }
</style>